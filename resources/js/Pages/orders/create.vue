<template>
    <div>
        <BaseDashboardHeader
        class="mt-3"
        showButton="true"
        title="Create Orders"
        navLinkName="orders.index"
        @search="search"
        NavLinkText="show all orders"
        :navs="[
            { name: 'home', linkName: 'dashboard' },
            { name: 'orders', linkName: 'orders.index' },
        ]"
    />
        <section class="bg-white py-8 antialiased dark:bg-gray-900 md:py-16">
            <form action="#" class="mx-auto max-w-screen-xl px-4 2xl:px-0">
                <div class="mx-auto max-w-3xl">
                    <div class="mt-6 sm:mt-8">
                        <div class="relative overflow-x-auto border-b border-gray-200 dark:border-gray-800">
                            <table class="w-full text-left font-medium text-gray-900 dark:text-white md:table-fixed">
                                <tbody class="divide-y divide-gray-200 dark:divide-gray-800">
                                    <tr v-for="(item, index) in Array(count).fill()" :key="index">
                                        <td class="whitespace-nowrap py-4">
                                            <div class="flex items-center gap-4">
                                                <div class="w-full mx-auto ml-4">
                                                    <label :for="'countries-' + index"
                                                        class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">
                                                        Select an option
                                                    </label>
                                                    <select :id="'countries-' + index"
                                                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                                                        <option disabled selected>Choose from the menu</option>
                                                        <option v-for="item in menuItems" :key="item.id" :value="item.id">{{ item.name }}</option>
                                                    </select>
                                                </div>
                                            </div>
                                        </td>

                                        <td class="p-4">
                                            <label for="quantity-input" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white ml-5">
                                                Choose quantity:
                                            </label>
                                            <div class="flex items-center justify-center max-w-[10rem] mx-auto">
                                                <button @click="decrement(index)" class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-s-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none">
                                                    <svg class="w-3 h-3 text-gray-900 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 18 2">
                                                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 1h16" />
                                                    </svg>
                                                </button>
                                                <input type="text" v-model="quantities[index]" data-input-counter
                                                    class="bg-gray-50 border-x-0 border-gray-300 h-11 w-16 text-center text-gray-900 text-sm focus:ring-blue-500 focus:border-blue-500 block py-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                                                    placeholder="999" required />
                                                <button @click="increment(index)" class="bg-gray-100 dark:bg-gray-700 dark:hover:bg-gray-600 dark:border-gray-600 hover:bg-gray-200 border border-gray-300 rounded-e-lg p-3 h-11 focus:ring-gray-100 dark:focus:ring-gray-700 focus:ring-2 focus:outline-none">
                                                    <svg class="w-3 h-3 text-gray-900 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 18 18">
                                                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 1v16M1 9h16" />
                                                    </svg>
                                                </button>
                                            </div>
                                        </td>

                                        <td class="p-4 text-right">
                                            <span class="block mb-2 text-sm font-medium text-gray-900 dark:text-white mr-2">Price</span>
                                            <span class="text-base font-bold text-gray-900 dark:text-white">
                                                $1,499
                                            </span>
                                        </td>
                                        <td class="p-4 text-right">
                                            <button @click.prevent="deleteItem(index)"
                                                class="text-red-600 hover:text-red-800 font-medium">
                                                Delete
                                            </button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>

                        <div class="mt-4 space-y-6 text-center">
                            <button @click="addItem"
                                class="text-xl font-semibold text-center text-gray-900 dark:text-white">
                                Add
                            </button>
                            <div class="space-y-4">
                                <dl
                                    class="flex items-center justify-between gap-4 border-t border-gray-200 pt-2 dark:border-gray-700">
                                    <dt class="text-lg font-bold text-gray-900 dark:text-white">Total</dt>
                                    <dd class="text-lg font-bold text-gray-900 dark:text-white">$7,191.00</dd>
                                </dl>
                            </div>
                            <div class="gap-4 sm:flex sm:items-center">
                                <button type="button"
                                    class="w-full rounded-lg border border-gray-200 bg-white px-5 py-2.5 text-sm font-medium text-gray-900 hover:bg-gray-100 hover:text-primary-700 focus:z-10 focus:outline-none focus:ring-4 focus:ring-gray-100 dark:border-gray-600 dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white dark:focus:ring-gray-700">Continue</button>
                            </div>
                        </div>
                    </div>
                </div>
            </form>
        </section>
    </div>
</template>


<script setup>
import { Head, Link } from "@inertiajs/vue3";
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import BaseDashboardHeader from "@/Components/BaseDashboardHeader.vue";
defineOptions({ layout: AuthenticatedLayout });
import { onMounted, ref } from 'vue';
import { initFlowbite } from 'flowbite';
onMounted(() => {
    initFlowbite();
});


const props = defineProps({
    menuItems: Object,
});

const count = ref(1);
const quantities = ref(Array(count.value).fill(1));

const addItem = () => {
    count.value++;
    quantities.value.push(1); 
};

const increment = (index) => {
    quantities.value[index]++;
};

const decrement = (index) => {
    if (quantities.value[index] > 1) {
        quantities.value[index]--;
    }
};

const deleteItem = (index) => {
    quantities.value.splice(index, 1); 
    count.value = quantities.value.length; 
};
</script>
