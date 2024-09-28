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
    <div class="sm:hidden fixed left-0 right-0 top-0 z-20 bg-white max-h-10">
      <div class="w-full p-1 z-20 bg-white relative">
        <div class="text-right mt-4 h-10">
          <Transition><i v-if="!showBurgerMenu" class="fa-solid fa-bars cursor-pointer text-xl absolute right-4" @click="openBurgerMenu"></i></Transition>
          <Transition><i v-if="showBurgerMenu" class="fa-solid fa-xmark cursor-pointer text-xl absolute right-4" @click="closeBurgerMenu"></i></Transition>      
        </div>  
        <h3 class="font text-xs text-center mt-2">Emily Rae Smith Labuschagne</h3>      
      </div>
      <Transition name="menuItems" :duration="550">
          <nav class="text-left pl-3 text-base pb-3 bg-white z-10 w-3/5 float-right h-screen bg-opacity-80" v-if="showBurgerMenu">
            <ul @click="closeBurgerMenu">
              <li class="mb-6 mt-8">
                <RouterLink class="ml-2 mr-2 hover:underline text-sm" to="/">Home</RouterLink>
              </li>
              <li class="mb-6">
                <RouterLink class="ml-2 mr-2 hover:underline text-sm" to="/available-works/all">Available Works</RouterLink>
              </li>
              <li class="mb-6">
                <RouterLink class="ml-2 mr-2 hover:underline text-sm" to="/about">About</RouterLink>
              </li>
              <li class="mb-6">
                <RouterLink class="ml-2 mr-2 hover:underline text-sm" to="/contact">Contact</RouterLink>
              </li>
            </ul>         
          </nav>
        </Transition>
    </div>
    <!-- End mobile screen nav -->
  </header>

  <RouterView class="mt-24"/>
</template>

<style scoped>
.router-link-active {
  color: #111827;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.menuItems-enter-active,
.menuItems-leave-active {
  transition: all 0.5s ease-in-out;
}

.menuItems-enter-from,
.menuItems-leave-to {
  transform: translateX(100px);
  opacity: 0;
}
</style>
