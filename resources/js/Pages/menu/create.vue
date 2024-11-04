<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head } from "@inertiajs/vue3";
import { onMounted, ref } from "vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import InputError from "@/Components/InputError.vue";
import { useForm } from "@inertiajs/vue3";
import Swal from "sweetalert2";
import { Link } from "@inertiajs/vue3";
import BaseDashboardHeader from "@/Components/BaseDashboardHeader.vue";
import { initFlowbite } from "flowbite";
defineOptions({ layout: AuthenticatedLayout });
defineProps({
    categories: Object,
});
onMounted(() => {
    initFlowbite();
});

const submit = () => {
    form.post(route("menu.store"), {
        preserveScroll: true,
        onSuccess: () =>
            Swal.fire({
                icon: "success",
                title: "success",
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
    price: "",
    category_id: "",
});
</script>

<template>
        <BaseDashboardHeader
        class="mt-3"
        showButton="true"
        title="Create Menu"
        navLinkName="categories.index"
        @search="search"
        NavLinkText="Show all menu items"
        :navs="[
            { name: 'home', linkName: 'dashboard' },
            { name: 'menu', linkName: 'categories.index' },
            { name: 'create', linkName: 'menu.create' },
        ]"
    />
    <section class="bg-white dark:bg-gray-900 h-screen">
        <div class="py-8 px-4 mx-auto max-w-2xl lg:py-16">
            <h2 class="mb-4 text-xl font-bold text-gray-900 dark:text-white">
                Add a new Item
            </h2>
            <form @submit.prevent="submit">
                <div class="grid gap-4 sm:grid-cols-2 sm:gap-6">
                    <div class="sm:col-span-2">
                        <label
                            for="name"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                            >Item Name</label
                        >
                        <input
                            type="text"
                            v-model="form.name"
                            name="name"
                            id="name"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
                            placeholder="item name"
                           
                        />
                        <InputError class="mt-2" :message="form.errors.name" />
                    </div>
                    <div class="w-full">
                        <label
                            for="price"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                            >Price</label
                        >
                        <input
                            type="number"
                            v-model="form.price"
                            name="price"
                            id="price"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
                            placeholder="$2999"
                            
                        />
                        <InputError class="mt-2" :message="form.errors.price" />
                    </div>
                    <div>
                        <label
                            for="category"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                            >Category</label
                        >
                        <select
                            id="category"
                            v-model="form.category_id"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-500 focus:border-primary-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
                        >
                            <option selected disabled :value="null">
                                Select category
                            </option>
                            <option
                                v-for="category in categories"
                                :value="category.id"
                                :key="category.id"
                            >
                                {{ category.name }}
                            </option>
                        </select>
                        <InputError
                            class="mt-2"
                            :message="form.errors.category_id"
                        />
                    </div>
                </div>
                <div class="mt-4 items-center">
                    <PrimaryButton>Add Item</PrimaryButton>
                </div>
            </form>
        </div>
    </section>
</template>
