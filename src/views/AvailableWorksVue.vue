<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router';

const images = ref([])
const artworkDetails = ref([])
const showPrices = ref(false)

function loadImages(){
  let artwork = []
  let artworkTemp = []
  images.value = import.meta.glob('/public/images/*.jpg')

  //loop through each image imported from the folder
  for(let path in images.value){
    artwork = []

    artwork.push(path.slice(7))
    artworkTemp = path.slice(15).split('-')
    artwork.push(artworkTemp[0])
    artwork.push(artworkTemp[1])
    artwork.push(artworkTemp[2])
    artwork.push(artworkTemp[3])

    artworkDetails.value.push(artwork)
  }
}


onMounted(() => {
    const route = useRoute()

    //only show prices if key is used in URL
    if(route.params.key === 'xF16LK'){
        showPrices.value = true
    }

    //load image details into an array and load artwork details into a nested array
    loadImages()
})

</script>

<template>
  <div
    class="flex justify-center flex-wrap sm:ml-4 sm:mr-4 md:ml-20 md:mr-20 lg:ml-40 lg:mr-40"
    v-viewer.static="{ transition: false, scalable: false, rotatable: false, fullscreen: false }"
  >
    <div v-for="artwork in artworkDetails" :key="artwork">
      <div
        class="h-60 w-60 p-2 ml-3 mr-3 mt-3 mb-1 border border-gray-300 bg-gray-100 rounded flex justify-center align-middle hover:cursor-pointer"
      >
        <img
          :src="artwork[0]"
          :alt="artwork[1]"
          class="max-w-full max-h-full rounded"
        />
      </div>
      <div class="p-1 ml-3 mr-3 mt-0 mb-3 border rounded text-center text-wrap w-60">  
        <p class="text-wrap">{{ artwork[1] }}</p>
        <p>{{ artwork[2] }}</p>
        <p>{{ artwork[3] }}</p>
        <p v-if="showPrices">{{ artwork[4] }}</p>
      </div>
    </div>
  </div>
</template>

<style></style>
