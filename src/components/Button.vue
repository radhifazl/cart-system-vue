<script setup>
defineProps({
    text: {
        type: String,
        default: 'Add to Cart'
    },
    cart: {
        type: Boolean,
        default: false
    }
})
</script>
<template>
    <button 
        @click="$emit('action')" 
        class="
            px-5 py-2 rounded-md bg-blue-400 hover:bg-blue-600 transition text-white
            border-none outline-none
        "
    >
        <span v-if="!cart">
            {{ text }}
        </span>
        <i class='bx bx-fw bx-cart-add' v-else></i>
    </button>
</template>
<style>
    
</style>