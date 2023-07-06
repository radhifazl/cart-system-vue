<script setup>
defineProps({
    status: {
        type: Boolean,
        default: false
    }
})
</script>

<template>
    <div class="w-fit max-md:w-full right-[50%] translate-x-[50%] rounded-md shadow-xl bg-green-300 p-5 py-4 font-bold absolute z-10"
        :class="{'translate-y-0': status, '-translate-y-20': !status, 'transition duration-500 ease-in-out': true}"
    >
        <i class='bx bx-fw bx-check-double'></i> Berhasil menambahkan produk ke keranjang!
    </div>
</template>

<style>
    
</style>