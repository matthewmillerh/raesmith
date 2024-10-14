<script setup>
import { onMounted, onUnmounted } from 'vue';

onMounted(() => {
    document.body.style.overflow = "hidden";
})

onUnmounted(() => {
    document.body.style.overflow = "scroll";
})
</script>

<template>
    <div class="bg-black bg-opacity-60 fixed left-0 right-0 top-0 bottom-0 z-30 flex justify-center items-center p-1 overscroll-contain overflow">
        <img src="/images/001-Title-Medium-Dimensions-Price-.jpg" alt="" class="max-w-[90%] max-h-full">
    </div>
</template>
<style>

</style>