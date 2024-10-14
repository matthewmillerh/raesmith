<script setup>
import ImageGallery from '@/components/ImageGallery.vue';
import { useRoute } from 'vue-router';
import { onBeforeMount, ref } from 'vue';

const showPrices = ref(false)

onBeforeMount(() => {
    const route = useRoute()

    //only show prices if key is used in URL
    if(route.params.key === 'xF16LK'){
        showPrices.value = true
    }
})
</script>
<template>
<div><ImageGallery image-folder="/public/images/*.jpg" :prices="showPrices"></ImageGallery></div>
</template>
  
<style></style>
  