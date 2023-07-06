<script setup>
import Button from './Button.vue';

const props = defineProps(['img', 'title', 'price', 'alt'])

</script>

<template>
    <div class="product-card rounded-md shadow-2xl p-2 w-[250px] h-[250px] bg-white grid place-items-center">
        <div class="product-card__detail h-full w-full overflow-hidden relative flex flex-col items-center text-gray-600">
            <div class="product-card__image w-full h-1/2 mb-5 flex items-center justify-center">
                <img :src="img" :alt="alt" width="50">
            </div>

            <h1 class="text-sm truncate overflow-hidden w-4/5">
                {{ title }}
            </h1>

            <div class="product-card__buttons w-full flex justify-between items-center absolute bottom-0 left-0">
                <p class="text-lg">
                    ${{ price }}
                </p>
                <Button 
                    :cart="true"
                    @action="$emit('cart')"
                />
            </div>
        </div>
    </div>
</template>
<style>
    
</style>