<script setup lang="ts">
import { Heart } from 'lucide-vue-next';
</script>

<template>
  <footer class="w-full py-20 flex flex-col items-center justify-center text-slate-500 font-sans relative z-10 mt-10">
    <!-- Starburst decorative -->
    <div class="w-16 h-1 bg-pink-headband/50 rounded-full mb-8"></div>
    
    <div class="flex items-center gap-3 bg-white/50 px-8 py-4 rounded-full shadow-lg border border-white backdrop-blur-md hover:scale-105 transition-transform duration-500 cursor-default">
      <Heart class="text-pink-400 animate-pulse" :size="24" fill="currentColor" />
      <span class="text-xl md:text-2xl font-bold tracking-widest text-[#a3a8ad]">
        辛苦了，之后的日子加油！
      </span>
      <Heart class="text-pink-400 animate-pulse" :size="24" fill="currentColor" />
    </div>

    <p class="mt-8 text-xs text-slate-400 tracking-wider">
      Made with Love & Vue 3
    </p>
  </footer>
</template>
