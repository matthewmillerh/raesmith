<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router';

const images = ref([])
const artworkDetails = ref([])
const showPrices = ref(false)

//import all the images from the available works image folder
function loadImages(){
  let artwork = []
  let artworkTemp = []
  images.value = import.meta.glob('/public/images/*.jpg')

  //loop through each image imported from the folder
  for(let path in images.value){
    //satrt each loop with a blank array
    artwork = []

    //split the image name into an array containing the artwork details
    artworkTemp = path.slice(15).split('-')

    //add each the artwork details to an array
    artwork.push(path.slice(7))    
    artwork.push(artworkTemp[0])
    artwork.push(artworkTemp[1])
    artwork.push(artworkTemp[2])
    artwork.push(artworkTemp[3])

    //add the array of artwork details to the main nested array of artworks
    artworkDetails.value.push(artwork)  
  }
}

//pass click event from overay to the underlying image to open it in v-viewer
const imageRef = ref({})
function clickImg(img){
  imageRef.value[img].click()
}

//variable to delay images being shown till mounted
const showImages = ref(false)

onMounted(() => {
    const route = useRoute()

    //only show prices if key is used in URL
    if(route.params.key === 'xF16LK'){
        showPrices.value = true
    }

    //load image details into an array and load artwork details into a nested array
    loadImages()

    //only show images after mount to prevent image press on mobile
    showImages.value = true;
})

</script>

<template>
  <div
    class="flex justify-center flex-wrap sm:ml-4 sm:mr-4 md:ml-20 md:mr-20 lg:ml-40 lg:mr-40 mt-14"
    v-viewer.static="{ transition: false, scalable: false, rotatable: false, fullscreen: false }"
  >
    <div v-for="artwork in artworkDetails" :key="artwork">
      <div
        class="max-h-96 max-w-72 p-2 ml-3 mr-3 mt-3 mb-1 border border-gray-300 bg-gray-50 rounded flex justify-center items-center hover:cursor-pointer relative object-contain aspect-[12/16]"
      >
        <img
          :src="artwork[0]"
          :alt="artwork[1]"
          class="max-w-full rounded flex justify-center align-middle ml-auto mr-auto"
          :ref="(el) => (imageRef[artwork[0]] = el)"
        />
        <!-- Information Block -->
         <div class="absolute top-0 left-0 bottom-0 right-0 transition-all duration-300 opacity-0 hover:opacity-100 rounded hover:bg-opacity-45 hover:bg-black text-white flex justify-end items-end" @click="clickImg(artwork[0])">
          <div class="p-2 text-xs">
            <p class="text-wrap text-right">{{ artwork[1] }}</p>
            <p class="text-right">{{ artwork[2] }}</p>
            <p class="text-right">{{ artwork[3] }}</p>
            <p v-if="showPrices" class="text-right">{{ artwork[4] }}</p>
          </div>          
         </div>       
      </div>

      <!-- Information Block -->
      <!-- <div class="p-1 ml-3 mr-3 mt-0 mb-3 border rounded text-center text-wrap w-60">  
        <p class="text-wrap">{{ artwork[1] }}</p>
        <p>{{ artwork[2] }}</p>
        <p>{{ artwork[3] }}</p>
        <p v-if="showPrices">{{ artwork[4] }}</p>
      </div> -->
    </div>
  </div>
</template>

<style>

</style>
