<script setup>
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Link, useForm, usePage } from '@inertiajs/vue3';

const props = defineProps({
    product: {
        type: Object,
    },
    imageClass: {
        type: String,
        default: 'h-48',
    },
    info: {
        type: String,
        default: '',
    },
});

const form = useForm({
    product_id: props.product.id,
});

const addItemToCart = () => {
    form.get(route('cart.add_product'), {
        preserveScroll: true,
    });
};
</script>

<template>
    <div class="p-0 bg-white dark:bg-gray-800 shadow sm:rounded-lg overflow-hidden">
        <img
            src="https://via.placeholder.com/600x400.png?text=Product" alt="Product Image"
            class="w-full object-cover"
            :class="imageClass">
        <div class="p-4">
            <h3
                class="font-semibold text-md text-gray-800 dark:text-gray-200 leading-tight"
            >
                Product Name
            </h3>
            <p class="text-sm text-gray-800 dark:text-gray-200">Product Description {{info}}</p>
            <p class="text-md font-medium text-gray-900 dark:text-gray-200">$19.99</p>
            <button
                type="button"
                class="mt-4 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                @click="addItemToCart"
            >Add to Cart</button>
        </div>
    </div>
</template>
