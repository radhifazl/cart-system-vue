<script setup>
defineProps(['text'])
</script>
<template>
    <button 
        @click="$emit('action')" 
        class="
            px-5 py-2 rounded-md bg-blue-400 hover:bg-blue-600 transition text-white
            border-none outline-none
        "
    >
        {{ text }}
    </button>
</template>
<style>
    
</style>