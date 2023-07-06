<script setup>
defineProps({
    totalProduct: {
        type: Number,
        default: 0
    }
})
</script>

<template>
    <div class="w-full flex justify-between">
        <h1 class=" text-gray-600 font-bold text-2xl mb-5">Cart System</h1>
        <button class=" bg-white text-slate-600 rounded-md shadow-xl p-3 hover:bg-gray-100 transition" @action="$emit('click')">
            <i class='bx bx-fw bx-cart'></i> -
            <span>{{ totalProduct }}</span>
        </button>
    </div>
</template>

<style>
    
</style>