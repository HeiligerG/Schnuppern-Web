<script setup>
import { ref } from 'vue'
import Header from './components/Header.vue'
import { RouterView } from 'vue-router';

const backgroundStyle = ref({
  background: ` url(https://www.transparenttextures.com/patterns/gplay.png)`,
  backgroundSize: '260px, auto',
  backgroundRepeat: 'repeat, no-repeat',
  display: 'block'
})
</script>

<template>
  <div class="relative h-screen w-screen">
    <!-- Gradient-Hintergrund -->
    <div class="absolute inset-0 bg-gradient-to-br from-sky-400 to-blue-800"></div>

    <!-- Textur-Overlay -->
    <div class="absolute inset-0" :style="backgroundStyle"></div>

    <!-- Inhalt -->
    <div class="relative z-10 w-full h-full flex flex-col items-center px-10 py-5 space-y-6 overflow-hidden">

      <RouterView />
    </div>
  </div>
</template>

<style scoped></style>
