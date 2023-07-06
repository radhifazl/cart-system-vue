<script setup>
defineProps({
    open: {
        type: Boolean,
        default: false
    }
})
</script>

<template>
    <div class="w-1/3 max-md:w-full bg-white fixed z-10 right-0 top-0 h-screen max-h-screen overflow-y-auto p-5 text-slate-700"
        :class="{'translate-x-0': open, 'translate-x-full': !open, 'transition duration-500 ease-in-out': true}"
    >
        <i class='bx bx-fw bx-x-circle pt-1 hover:text-red-400 cursor-pointer transition  z-10 relative'
            @click="$emit('close')"
        ></i>
        <div class="h-full w-full flex justify-center">
            <slot />
        </div>
    </div>
</template>

<style>
    
</style>