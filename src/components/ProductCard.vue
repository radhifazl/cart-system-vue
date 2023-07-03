<script setup>
import Button from './Button.vue';

const props = defineProps(['img', 'title', 'price', 'alt'])

</script>

<template>
    <div class="product-card rounded-md shadow-2xl p-5 w-[250px] h-[250px] bg-white grid place-items-center">
        <div class="product-card__detail w-full flex flex-col justify-center items-center gap-5 text-gray-600">
            <div class="product-card__image">
                <img :src="img" :alt="alt" width="50">
            </div>

            <h1 class="text-sm">
                {{ title }}
            </h1>

            <div class="product-card__buttons w-full flex justify-between items-center">
                <p class="text-lg">
                    ${{ price }}
                </p>
                <Button 
                    text="Add"
                    @action="$emit('cart')"
                />
            </div>
        </div>
    </div>
</template>
<style>
    
</style>