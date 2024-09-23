<script setup>
const images = import.meta.glob('@/assets/images/*.jpg')

console.log(images)
</script>

<template>
    <div class="flex justify-center flex-wrap md:ml-60 md:mr-60 lg:ml-80 lg:mr-80" v-viewer.static="{transition: false, scalable: false, rotatable: false, fullscreen: false}">
        <div v-for="image in images" :key="image">
            <div class="">
                <img :src="'.' + image.name" alt="Emily" class="h-40 w-32 p-1 m-3 border border-gray-300 bg-gray-100 rounded">
            </div>      
        </div>
    </div>
</template>

<style>
</style>