<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <div class="w-full min-h-24 p-1 border-b border-black mb-4">
        <h3 class="font-semibold text-2xl text-center mt-2">Emily Rae Smith Labuschagne</h3>
        <nav class="text-center mt-3 text-base">
          <RouterLink class="ml-2 mr-2 hover:underline" to="/">Home</RouterLink>
          <RouterLink class="ml-2 mr-2 hover:underline" to="/available-works/all"
            >Available Works</RouterLink
          >
          <RouterLink class="ml-2 mr-2 hover:underline" to="/about">About</RouterLink>
          <RouterLink class="ml-2 mr-2 hover:underline" to="/contact">Contact</RouterLink>
        </nav>
      </div>
    </div>
    <!-- End Wrapper -->
  </header>

  <RouterView />
</template>

<style scoped>
.router-link-active {
  text-decoration: underline;
}
</style>
