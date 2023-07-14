<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import DeleteUserForm from './Partials/DeleteUserForm.vue';
import UpdatePasswordForm from './Partials/UpdatePasswordForm.vue';
import UpdateProfileInformationForm from './Partials/UpdateProfileInformationForm.vue';
import ProductCard from './Partials/ProductCard.vue';
import { Head } from '@inertiajs/vue3';
import { ref } from 'vue';

const props = defineProps({
    latestProducts: {
        type: Object,
    },
    products: {
        type: Object,
    },
    cartItems: {
        type: Object,
    },
    user: {
        type: Object,
    },
});

let latestProductsIndexStart = ref(0);
const cartItems = ref(props.cartItems ?? []);

</script>

<template>
    <Head title="Produtos" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Produtos</h2>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Cart: <span v-text="cartItems.length"></span></h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 space-y-6">

                <div class="pt-4">
                    <h2
                        class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight pb-4"
                    >
                        Products
                    </h2>
                    <div
                        class="grid grid-cols-3 gap-3 sm:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 p-0"
                    >
                        <template
                            v-for="product in products.data"
                            :key="product.id"
                        >
                            <ProductCard
                                :product="product"
                            />
                        </template>
                    </div>
                </div>

                <div class="pt-4">
                    <h2
                        class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight pb-4"
                    >
                        Latest products
                    </h2>

                    <div class="carousel relative overflow-hidden nowrap">
                        <div class="carousel-inner relative w-full">
                          <div class="carousel-item">
                            <div class="grid grid-cols-6 gap-4 no-gutters nowrap">
                                <template
                                    v-for="(product, index) in latestProducts"
                                    :key="product.id"
                                >
                                    <ProductCard
                                        class="col-span-3 sm:col-span-3 md:col-span-2 lg:col-span-1"
                                        :product="product"
                                        image-class="h-24"
                                        :info="`${index} | ${latestProducts.length} | ${latestProductsIndexStart}`"
                                        v-if="index >= latestProductsIndexStart && index <= (latestProductsIndexStart + 5)"
                                    />
                                </template>
                            </div>
                          </div>
                        </div>

                        <div class="carousel-controls absolute top-0 w-full flex justify-between items-center">
                            <button
                                type="button"
                                @click="latestProductsIndexStart = latestProductsIndexStart == 0 ? 0 : latestProductsIndexStart - 1"
                                class="carousel-control-prev w-16 h-16 bg-gray-900 text-white rounded-full hover:bg-gray-700 focus:outline-none focus:bg-gray-700"
                            >
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                                <path fill-rule="evenodd" d="M11.707 4.293a1 1 0 0 0-1.414 0L5.586 9.586a2 2 0 0 0 0 2.828l4.707 4.707a1 1 0 1 0 1.414-1.414L8.414 12H16a1 1 0 1 0 0-2H8.414l3.293-3.293a1 1 0 0 0 0-1.414z" clip-rule="evenodd" />
                                </svg>
                            </button>
                            <button
                                type="button"
                                @click="latestProductsIndexStart = (latestProductsIndexStart >= (latestProducts.length -1)
                                    ? (latestProducts.length -1) : latestProductsIndexStart + 1)"
                                class="carousel-control-next w-16 h-16 bg-gray-900 text-white rounded-full hover:bg-gray-700 focus:outline-none focus:bg-gray-700"
                                >
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                                <path fill-rule="evenodd" d="M8.293 4.293a1 1 0 0 1 1.414 0L14.414 9.586a2 2 0 0 1 0 2.828l-4.707 4.707a1 1 0 1 1-1.414-1.414L11.586 12H4a1 1 0 1 1 0-2h7.586l-3.293-3.293a1 1 0 0 1 0-1.414z" clip-rule="evenodd" />
                                </svg>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
