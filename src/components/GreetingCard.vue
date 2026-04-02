<script setup lang="ts">
import { Heart } from 'lucide-vue-next'
</script>

<template>
  <footer class="w-full py-20 flex flex-col items-center justify-center font-sans relative z-10">
    <!-- Greeting Card Design -->
    <div
      class="w-[90%] max-w-3xl bg-white rounded-lg shadow-[0_20px_50px_-12px_rgba(0,0,0,0.1)] border border-slate-100 p-2 transform hover:-translate-y-2 transition-all duration-500 overflow-hidden relative group"
    >
      <!-- Card inner border -->
      <div class="absolute inset-4 border border-pink-200/60 rounded z-0 pointer-events-none"></div>

      <!-- Content wrapper -->
      <div
        class="relative z-10 bg-[#FFFAF0] m-3 rounded flex flex-col md:flex-row items-center p-8 md:p-12 gap-8 md:gap-12 shadow-inner border border-slate-50"
      >
        <!-- Left: Image Section -->
        <div class="w-full md:w-1/2 flex items-center justify-center">
          <div
            class="bg-white p-1 shadow-md border border-slate-200 rounded transform -rotate-3 group-hover:rotate-0 transition-transform duration-500"
          >
            <div class="overflow-hidden rounded border border-slate-100 aspect-4/3 bg-slate-50">
              <!-- image placeholder -->
              <img
                src="/public/pics/图3.png"
                alt="Special Memory"
                class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-[2s] opacity-90"
              />
            </div>
          </div>
        </div>

        <!-- Right: Message Section -->
        <div
          class="w-full md:w-1/2 flex flex-col items-center md:items-start text-center md:text-left gap-6"
        >
          <div class="w-12 h-[2px] bg-pink-300 rounded mb-2"></div>

          <h2 class="font-handwriting text-4xl leading-relaxed text-slate-700 font-bold">
            辛苦了，<br />之后的日子<span class="text-pink-400">加油！</span>
          </h2>

          <p class="font-sans text-slate-400 leading-loose tracking-wide text-sm font-light">
            愿所有的美好如期而至，<br />
            愿未来的风景更加绚丽。<br />
            生日，快乐 ❤
          </p>

          <div class="mt-4 flex items-center gap-2">
            <Heart class="text-pink-400 animate-pulse" :size="20" fill="currentColor" />
            <Heart
              class="text-pink-300 animate-pulse"
              :size="16"
              fill="currentColor"
              style="animation-delay: 0.5s"
            />
            <Heart
              class="text-pink-200 animate-pulse"
              :size="12"
              fill="currentColor"
              style="animation-delay: 1s"
            />
          </div>
        </div>
      </div>
    </div>

    <!-- Final small text -->
    <p class="mt-12 text-xs text-slate-400 tracking-wider font-sans">Made with Love • For You</p>
  </footer>
</template>
