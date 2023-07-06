<script setup>
const props = defineProps(['img', 'title', 'price', 'alt', 'quantity'])
</script>

<template>
    <div 
        class="
            cart w-full h-[150px] rounded-md px-4 py-3 shadow-xl flex justify-between items-center
            bg-white text-gray-600 mb-5 border-gray-200 border
        "
    
    >
        <div class="delete">
            <button @click="$emit('delete')"
                class="
                    px-2 py-1 rounded-md bg-red-400 hover:bg-red-600 transition 
                    text-white border-none outline-none
                "
            >
                X
            </button>
        </div>

        <div class="img">
            <img :src="img" :alt="alt" width="50">
        </div>

        <div class="detail w-1/2">
            <h1 class="text-xs">
                {{ title }}
            </h1>

            <p class="text-sm my-3">
                ${{ price }}
            </p>

            <div class="addQuantityButtons w-full flex justify-between items-center gap-5">
                <button @click="$emit('subQty')"
                    class="
                        w-[50%] px-2 py-1 rounded-md bg-blue-400 hover:bg-blue-600 transition 
                        text-white border-none outline-none
                    "
                >
                    -
                </button>
                
                <p class="text-sm">
                    {{ quantity }}
                </p>

                <button @click="$emit('addQty')"
                    class="
                        w-[50%] px-2 py-1 rounded-md bg-blue-400 hover:bg-blue-600 transition 
                        text-white border-none outline-none
                    "
                >
                    +
                </button>
            </div>
        </div>
    </div>
</template>
<style>
    
</style>