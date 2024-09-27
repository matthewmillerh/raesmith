<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { ref } from 'vue'

const showBurgerMenu = ref(false)

function openBurgerMenu(){
  showBurgerMenu.value = true
}

function closeBurgerMenu(){
  showBurgerMenu.value = false
}


</script>

<template>
  <header>
    <!-- Large screen nav -->
    <div class="hidden sm:block">
      <div class="w-full min-h-24 p-1 border-b border-black mb-4">
        <h3 class="font-semibold text-2xl text-center mt-2">Emily Rae Smith Labuschagne</h3>
        <nav class="text-center mt-3 text-base">
          <RouterLink class="ml-2 mr-2 hover:underline" to="/">Home</RouterLink>
          <RouterLink class="ml-2 mr-2 hover:underline" to="/available-works/all">Available Works</RouterLink>
          <RouterLink class="ml-2 mr-2 hover:underline" to="/about">About</RouterLink>
          <RouterLink class="ml-2 mr-2 hover:underline" to="/contact">Contact</RouterLink>
        </nav>
      </div>
    </div>
    <!-- End Large screen nav -->

    <!-- Mobile screen nav -->
    <div class="sm:hidden fixed left-0 right-0 top-0 z-10 bg-white">
      <div class="w-full p-1">
        <h3 class="font-semibold text-sm text-center mt-2">Emily Rae Smith Labuschagne</h3>
        <div class="text-right -mt-6 h-10">
          <Transition><i v-if="!showBurgerMenu" class="fa-solid fa-bars cursor-pointer text-2xl absolute right-2" @click="openBurgerMenu"></i></Transition>
          <Transition><i v-if="showBurgerMenu" class="fa-solid fa-xmark cursor-pointer text-2xl absolute right-2" @click="closeBurgerMenu"></i></Transition>      
        </div>
        <Transition>
          <nav class="text-center mt-1 text-base transition-all" v-if="showBurgerMenu">
            <ul @click="closeBurgerMenu">
              <li class="mb-3">
                <RouterLink class="ml-2 mr-2 hover:underline" to="/">Home</RouterLink>
              </li>
              <li class="mb-3">
                <RouterLink class="ml-2 mr-2 hover:underline" to="/available-works/all">Available Works</RouterLink>
              </li>
              <li class="mb-3">
                <RouterLink class="ml-2 mr-2 hover:underline" to="/about">About</RouterLink>
              </li>
              <li>
                <RouterLink class="ml-2 mr-2 hover:underline" to="/contact">Contact</RouterLink>
              </li>
            </ul>         
          </nav>
        </Transition>
        
      </div>
    </div>
    <!-- End mobile screen nav -->
  </header>

  <RouterView />
</template>

<style scoped>
.router-link-active {
  text-decoration: underline;
}

/* we will explain what these classes do next! */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
