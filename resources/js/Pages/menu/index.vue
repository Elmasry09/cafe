<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import BaseDashboardHeader from '@/Components/BaseDashboardHeader.vue';
import { Link, router } from "@inertiajs/vue3";
import Swal from 'sweetalert2'
import paginate from '@/Components/paginate.vue';

defineOptions({ layout: AuthenticatedLayout });

defineProps({
    menuItems: Object
});

const deleteItem = (id) => {
    Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!'
    }).then((result) => {
        if (result.isConfirmed) {
            router.delete(route('menu.destroy', id), {
                preserveScroll: true,
                onSuccess: () => Swal.fire({
                    icon: 'success',
                    title: 'success',
                    text: 'Item deleted successfully',
                })
            })
        }
    })
}

function search(value) {
  router.get(
    route("students.index"),
    { search: value },
    {
      preserveState: true,
      replace: true,
    }
  );
}

</script>

<template>

<BaseDashboardHeader
    class="mt-3"
    addSearchInput="false"
    title="Menu"
    navLinkName="menu.create"
    @search="search"
    NavLinkText="Add new menu item"
    :navs="[
      { name: 'home', linkName: 'dashboard' },
      { name: 'menu', linkName: 'menu.index' },
    ]"
  />

    <div  v-if="menuItems" class="container my-5 py-5 mx-auto px-4 md:px-6 lg:px-12">
        <!--Section: Design Block-->
        <section class="mb-20 text-gray-800">
            <div class="block rounded-lg shadow-lg bg-white">
                <div class="flex flex-col">
                    <div class="overflow-x-auto sm:-mx-6 lg:-mx-8">
                        <div class="inline-block min-w-full sm:px-6 lg:px-8">
                            <div class="overflow-hidden">
                                <table class="min-w-full mb-0">
                                    <thead class="border-b bg-gray-50 rounded-t-lg text-left">
                                        <tr>
                                            <th scope="col" class="rounded-tl-lg text-sm font-medium px-6 py-4">
                                                NAME
                                            </th>
                                            <th scope="col" class="text-sm font-medium px-6 py-4">
                                                Price
                                            </th>
                                            <th scope="col" class="rounded-tr-lg text-sm font-medium px-6 py-4">
                                                Actions
                                            </th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr class="border-b" v-for="(item) in menuItems.data" :key="item.id">
                                            <th scope="row"
                                                class="text-sm font-normal px-6 py-4 whitespace-nowrap text-left">
                                                <div class="flex flex-row items-center">
                                                    <div class="ml-4">
                                                        <p class="mb-0.5 font-medium">
                                                            {{ item.name }}
                                                        </p>
                                                    </div>
                                                </div>
                                            </th>
                                            <td class="text-sm font-normal px-6 py-4 whitespace-nowrap text-left">
                                                <div class="flex flex-col">
                                                    <p class="mb-0.5">
                                                        {{ item.price }}
                                                    </p>
                                                </div>
                                            </td>
                                            <td
                                                class="align-middle text-sm font-normal px-6 py-4 whitespace-nowrap text-left">
                                                    <Link :href="route('menu.edit', item.slug)"
                                                        class="font-medium px-2 text-green hover:text-green-dark hover:scale-105 transition ease-in-out duration-200">
                                                    Edit</Link>
                                                <Link @click="deleteItem(item.slug)" as="button"
                                                    class="font-medium text-red-500 hover:text-red-700 hover:scale-105 transition ease-in-out duration-200">
                                                delete</Link>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <paginate :items="menuItems" />

        <!--Section: Design Block-->
    </div>
</template>

<style lang="scss" scoped></style>