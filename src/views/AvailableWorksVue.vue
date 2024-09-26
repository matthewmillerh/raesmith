<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router';

const images = import.meta.glob('/public/images/*.jpg')
console.log(images)

//image details
const imageTitle = ref()
const imageMedium = ref()
const imageDimensions = ref()
const imagePrice = ref()

//gets the artwork details for the current image
function getArtworkDetails(image){
    let details = image.slice(15).split('-')

    imageTitle.value = details[0]
    imageMedium.value = details[1]
    imageDimensions.value = details[2]
    imagePrice.value = details[3]
}

//returns the usable image URL
function getImageURL(image) {
  return image.slice(7)
}

//returns details about the image from the name
//needs to be optimised
function imageDetails(image, index) {
  return image.slice(15).split('-')[index]
}

const showPrices = ref(false)
onMounted(() => {
    const route = useRoute()

    //only show prices if key is used in URL
    if(route.params.key === 'xF16LK'){
        showPrices.value = true
    }
})

</script>

<template>
  <div
    class="flex justify-center flex-wrap sm:ml-4 sm:mr-4 md:ml-20 md:mr-20 lg:ml-40 lg:mr-40"
    v-viewer.static="{ transition: false, scalable: false, rotatable: false, fullscreen: false }"
  >
    <div v-for="image in images" :key="image">
        {{ getArtworkDetails(image.name) }}
      <div
        class="h-60 w-60 p-2 ml-3 mr-3 mt-3 mb-1 border border-gray-300 bg-gray-100 rounded flex justify-center align-middle hover:cursor-pointer"
      >
        <img
          :src="getImageURL(image.name)"
          :alt="imageDetails(image.name, 0)"
          class="max-w-full max-h-full rounded"
        />
      </div>
      <div class="p-1 ml-3 mr-3 mt-0 mb-3 border rounded text-center text-wrap w-60">  
        <p class="text-wrap">{{ imageTitle }}</p>
        <p>{{ imageMedium }}</p>
        <p>{{ imageDimensions }}</p>
        <p v-if="showPrices">{{ imagePrice }}</p>
        <!-- <p>{{ imageDetails(image.name, 0) }}</p>
        <p>{{ imageDetails(image.name, 1) }}</p>
        <p>{{ imageDetails(image.name, 2) }}</p>
        <p>{{ imageDetails(image.name, 3) }}</p> -->
      </div>
    </div>
  </div>
</template>

<style></style>
