<script setup>
import Header from '../components/Header.vue'
</script>

<template>
  <div class="min-h-screen flex flex-col items-center">
    <!-- Header -->
    <Header />

    <!-- Content Wrapper -->
    <div
      class="relative max-w-full md:max-w-[80%] lg:max-w-[50%] bg-white rounded-xl shadow-xl p-8 mt-12 md:mt-6 text-center"
    >
      <p class="text-gray-800 text-lg leading-relaxed">
        Diese Webseite ist für Schnupperlernende und Einsteiger gedacht, die JavaScript lernen
        möchten. Mit einfachen Erklärungen und praktischen Übungen bekommst du einen leichten
        Einstieg in die Programmierung. Schritt für Schritt kannst du eigene kleine Programme
        schreiben und dein Wissen vertiefen. Entdecke die spannende Welt von JavaScript und probiere
        es selbst aus!
      </p>

      <!-- Button Section -->
      <button
        @click="$router.push('/task/1')"
        class="mt-6 bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 px-6 rounded-lg flex items-center shadow-md transition-all mx-auto"
      >
        <svg
          class="w-6 h-6 mr-2"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M5 13l4 4L19 7"
          ></path>
        </svg>
        Los geht's
      </button>
    </div>
  </div>
</template>
