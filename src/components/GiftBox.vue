<script setup lang="ts">
import { ref } from 'vue'
import { Gift } from 'lucide-vue-next'

const emit = defineEmits(['opened'])
const isOpening = ref(false)

const openBox = () => {
  if (isOpening.value) return
  isOpening.value = true
  setTimeout(() => {
    emit('opened')
  }, 100)
}
</script>

<template>
  <div class="flex flex-col items-center justify-center min-h-screen w-full relative z-10">
    <div
      @click="openBox"
      class="cursor-pointer transition-all duration-700 ease-out"
      :class="{
        'scale-[2] opacity-0 filter blur-md': isOpening,
        'hover:scale-105 animate-wobble': !isOpening,
      }"
    >
      <div
        class="relative bg-white/80 backdrop-blur-sm p-12 rounded-[2.5rem] shadow-xl border border-pink-100 flex flex-col items-center gap-6 group hover:shadow-2xl transition-all duration-500"
      >
        <div
          class="absolute -top-5 bg-pink-headband text-white px-6 py-2 rounded-full text-sm font-bold shadow-pink-headband/50 shadow-lg tracking-wider z-10 border-2 border-white"
        >
          To MeowLynSea
        </div>

        <Gift
          :size="120"
          class="text-pink-headband group-hover:text-pink-400 group-hover:scale-110 transition-all duration-500 relative z-10 drop-shadow-md"
          stroke-width="1.5"
        />

        <h2 class="text-3xl font-sans text-slate-700 tracking-wide relative z-10 mt-2">
          打开礼物吧~❤
        </h2>
        <p class="text-pink-400 font-handwriting text-3xl -mt-4 relative z-10">
          A Gift From Little Wolf Me
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes wobble {
  0%,
  100% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(-1deg);
  }
  75% {
    transform: rotate(1deg);
  }
}
.animate-wobble {
  animation: wobble 5s ease-in-out infinite;
}
</style>
