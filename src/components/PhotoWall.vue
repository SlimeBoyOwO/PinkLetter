<script setup lang="ts">
import { Camera, Paperclip } from 'lucide-vue-next'

// We have 6 images, we will repeat them to get 8
const baseImages = [
  { src: '/PinkLetter/pics/pic7.jpg', label: '超美丽Beta写真' },
  { src: '/PinkLetter/pics/pic2.png', label: '我真是太抬举你了.jpg' },
  { src: '/PinkLetter/pics/pic8.jpg', label: '欲求不满的时候' },
  { src: '/PinkLetter/pics/pic9.png', label: '可以来找我要❤' },

  { src: '/PinkLetter/pics/毛衣.png', label: '送你的毛衣捏' },
  { src: '/PinkLetter/pics/pic6.jpg', label: '希望兔兔和你一起过生日' },
  { src: '/PinkLetter/pics/链接.png', label: '钦杯合体！' },
  { src: '/PinkLetter/pics/珍猪.jpg', label: '你永远是那颗珍猪~' },
]

// Generate 8 photos
const photos = Array.from({ length: 8 }).map((_, i) => baseImages[i % baseImages.length])

// We need 2 rows
const rows = [0, 1]
</script>

<template>
  <section class="w-full max-w-[1400px] mx-auto px-4 flex flex-col items-center gap-32 relative z-10 py-10">
    <!-- 4 Rows -->
    <div v-for="rowIndex in rows" :key="'row-' + rowIndex" class="relative w-full flex justify-center">
      <!-- Hanging String (Arc pointing down) -->
      <div
        class="absolute top-0 left-[-5%] right-[-5%] h-32 border-b-2 border-slate-400/60 rounded-[100%] pointer-events-none z-0">
      </div>

      <!-- LED String Lights (Pink Glowing Flowers) -->
      <div class="absolute top-0 left-[-5%] right-[-5%] h-32 pointer-events-none z-10 flex justify-evenly items-end">
        <div v-for="n in 6" :key="'led-' + rowIndex + '-' + n" class="relative flex items-center justify-center" :style="{
          transform: `translateY(${Math.abs(n - 6.5) * -5 + 10}px)`, // roughly follows the arc
        }">
          <!-- Custom SVG Flower (No Stem, Only Petals) -->
          <svg width="36" height="36" viewBox="0 0 100 100"
            class="text-pink-300 drop-shadow-[0_0_10px_rgba(244,114,182,0.8)] transition-transform hover:scale-110">
            <!-- 8 Petals -->
            <circle cx="50" cy="22" r="22" fill="currentColor" />
            <circle cx="50" cy="78" r="22" fill="currentColor" />
            <circle cx="22" cy="50" r="22" fill="currentColor" />
            <circle cx="78" cy="50" r="22" fill="currentColor" />
            <circle cx="30" cy="30" r="22" fill="currentColor" />
            <circle cx="70" cy="70" r="22" fill="currentColor" />
            <circle cx="30" cy="70" r="22" fill="currentColor" />
            <circle cx="70" cy="30" r="22" fill="currentColor" />
          </svg>

          <!-- Glowing Center -->
          <div
            class="absolute w-3 h-3 rounded-full bg-white shadow-[0_0_15px_8px_rgba(255,255,255,0.9)] animate-pulse z-10"
            :style="{
              animationDelay: `${Math.random() * 2}s`,
              animationDuration: `${1.5 + Math.random()}s`,
            }"></div>
        </div>
      </div>

      <!-- 4 Photos per row -->
      <div class="w-full flex justify-around items-start relative z-20 px-8" style="margin-top: 8rem">
        <div v-for="(photo, colIndex) in photos.slice(rowIndex * 4, rowIndex * 4 + 4)"
          :key="'photo-' + rowIndex + '-' + colIndex"
          class="relative group transition-all duration-300 hover:z-30 flex flex-col items-center" :class="{
            'mt-4': colIndex === 0 || colIndex === 3, // outer photos are higher due to arc
            'mt-12': colIndex === 1 || colIndex === 2, // inner photos are lower due to arc
          }" :style="{
            transform: `rotate(${Math.random() * 10 - 5}deg)`, // random rotation between -5 and 5
          }">
          <!-- The string connecting to the photo -->
          <div class="absolute -top-12 left-1/2 transform -translate-x-1/2 w-[2px] h-12 bg-slate-300/80"></div>
          <Paperclip class="absolute -top-5 left-1/2 transform -translate-x-1/2 text-slate-400 shadow-sm z-20"
            :size="24" stroke-width="1.5"
            :style="{ transform: `translateX(-50%) rotate(${Math.random() * 30 - 15}deg)` }" />

          <!-- Polaroid Frame -->
          <div
            class="bg-white p-3 pb-12 shadow-lg hover:shadow-2xl hover:scale-110 transition-all duration-300 border border-slate-100 rounded w-44 md:w-56">
            <div
              class="w-full aspect-square bg-slate-50 flex flex-col items-center justify-center overflow-hidden border border-slate-200 relative">
              <img :src="photo?.src" :alt="photo?.label"
                class="w-full h-full object-cover mix-blend-multiply opacity-90 group-hover:opacity-100 transition-opacity" />
              <div
                class="absolute inset-0 bg-pink-300/10 opacity-0 group-hover:opacity-100 transition-opacity pointer-events-none">
              </div>
            </div>
            <p
              class="font-handwriting text-center text-slate-500 text-lg md:text-xl absolute bottom-3 w-full left-0 tracking-widest bg-white/50 backdrop-blur-sm">
              {{ photo?.label }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Any specific scoped styles can go here if needed */
</style>
