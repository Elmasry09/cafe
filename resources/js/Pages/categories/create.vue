<template>
        <BaseDashboardHeader
        class="mt-2"
        showButton="true"
        title="Create Category"
        navLinkName="categories.index"
        @search="search"
        NavLinkText="Show all categories"
        :navs="[
            { name: 'home', linkName: 'dashboard' },
            { name: 'categories', linkName: 'categories.index' },
            { name: 'create', linkName: 'categories.create' },
        ]"
    />
<section class="bg-white dark:bg-gray-900 h-screen">
  <div class="py-8 px-4 mx-auto max-w-2xl lg:py-16">
      <form @submit.prevent="submit">
          <div class="grid gap-4 sm:grid-cols-2 sm:gap-6">
              <div class="sm:col-span-2">
                  <label for="name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Category Name</label>
                  <input type="text" v-model="form.name" name="name" id="name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500" placeholder="category name" required="">
                  <InputError class="mt-2" :message="form.errors.name" />
                </div>
          </div>
          <div class="mt-6 p-4">
              <PrimaryButton @click="submit">Add Category</PrimaryButton>
          </div>
      </form>
  </div>
</section>
</template>

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import InputError from "@/Components/InputError.vue";
import { useForm } from "@inertiajs/vue3";
import BaseDashboardHeader from '@/Components/BaseDashboardHeader.vue';
import Swal from 'sweetalert2'

defineOptions({ layout: AuthenticatedLayout });


const submit = () => {
    form.post(route("categories.store"), {
        preserveScroll: true,
        onSuccess: () =>
            Swal.fire({
                icon: "success",
                title: "category created successfully",
            }),
        onError: () =>
            Swal.fire({
                icon: "error",
                title: "error",
            }),
    });
};

const form = useForm({
    name: "",
});

</script>

<style lang="scss" scoped></style>