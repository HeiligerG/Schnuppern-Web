<script setup>
import { ref } from 'vue'

const backUpTitle = ref('Cooler Titel :D')
const title = ref('')
const speed = 150

const animateTitle = (forward = true, callback) => {
  let i = forward ? 0 : title.value.length
  const txt = backUpTitle.value

  const step = () => {
    if (forward ? i < txt.length : i > 0) {
      title.value = forward ? txt.substring(0, i + 1) : txt.substring(0, i - 1)
      i += forward ? 1 : -1
      setTimeout(step, speed)
    } else if (callback) {
      callback()
    }
  }
  step()
}

setTimeout(() => {
  animateTitle(true, () => {
    setTimeout(() => animateTitle(false), 7000)
  })
  setInterval(() => {
    animateTitle(true, () => {
      setTimeout(() => animateTitle(false), 7000)
    })
  }, 12500)
}, 2000)
</script>

<template>
  <header class="relative w-full max-w-2xl h-32 flex items-center justify-center mt-12">
    <div
      class="absolute w-full h-full bg-white opacity-20 border border-blue-300 rounded-xl shadow-lg"
    ></div>
    <h1 class="relative text-center text-3xl font-bold text-white font-mono z-10">
      {{ title }} <span class="blinking-cursor -ml-3">|</span>
    </h1>
  </header>
</template>

<style scoped>
.blinking-cursor {
  animation: blink 1s steps(2, start) infinite;
}

@keyframes blink {
  0% {
    opacity: 1;
  }
  20% {
    opacity: 1;
  }
  25% {
    opacity: 0;
  }
  75% {
    opacity: 0;
  }
  80% {
    opacity: 1;
  }
  100% {
    opacity: 1;
  }
}
</style>
