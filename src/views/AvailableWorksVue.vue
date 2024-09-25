<script setup>
import { onMounted, ref } from 'vue'

const images = import.meta.glob('/public/images/*.jpg')
console.log(images)

const showPrices = ref(null)

//returns the usable image URL
function imageURL(image) {
  return image.slice(7)
}

//returns details about the image from the name
//needs to be optimised
function imageDetails(image, index) {
  return image.slice(15).split('-')[index]
}

onMounted(() => {
  showPrices.value = route.params.key
})
</script>

<template>
  <div
    class="flex justify-center flex-wrap sm:ml-4 sm:mr-4 md:ml-20 md:mr-20 lg:ml-40 lg:mr-40"
    v-viewer.static="{ transition: false, scalable: false, rotatable: false, fullscreen: false }"
  >
    <div v-for="image in images" :key="image">
      <div
        class="h-60 w-60 p-2 ml-3 mr-3 mt-3 mb-1 border border-gray-300 bg-gray-100 rounded flex justify-center align-middle"
      >
        <img
          :src="imageURL(image.name)"
          :alt="imageDetails(image.name, 0)"
          class="max-w-full max-h-full rounded"
        />
      </div>
      <div class="p-1 ml-3 mr-3 mt-0 mb-3 border rounded text-center">
        <p>{{ imageDetails(image.name, 0) }}</p>
        <p>{{ imageDetails(image.name, 1) }}</p>
        <p>{{ imageDetails(image.name, 2) }}</p>
        <p v-if="showPrices === 'xF16LK'">{{ imageDetails(image.name, 3) }}</p>
      </div>
    </div>
  </div>
</template>

<style></style>
