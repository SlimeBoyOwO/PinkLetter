<script setup lang="ts">
import { ref } from 'vue'
import { Play, Pause, Volume2, Heart } from 'lucide-vue-next'

const isPlaying = ref(false)
const audioRef = ref<HTMLAudioElement | null>(null)

const togglePlay = () => {
  if (!audioRef.value) return

  if (isPlaying.value) {
    audioRef.value.pause()
    isPlaying.value = false
  } else {
    audioRef.value
      .play()
      .then(() => {
        isPlaying.value = true
      })
      .catch((e) => {
        console.warn(
          'Please add your music file! Expected at /music.mp3 or change the src below.',
          e,
        )
        isPlaying.value = true
      })
  }
}

// 添加一个专门用于外部调用的播放函数
const playMusic = () => {
  if (!audioRef.value) return

  // 如果已经在播放，就不重复播放
  if (isPlaying.value) return

  audioRef.value
    .play()
    .then(() => {
      isPlaying.value = true
    })
    .catch((e) => {
      console.warn('Please add your music file! Expected at /music.mp3 or change the src below.', e)
    })
}

// 暴露playMusic函数供父组件调用
defineExpose({
  playMusic,
})
</script>

<template>
  <div
    class="flex flex-col md:flex-row items-center justify-center gap-14 lg:gap-24 w-full max-w-7xl mx-auto px-4 mt-6"
  >
    <!-- LEFT SIDE DECORATIONS: Balloons & Sleeping Cat -->
    <div
      class="hidden md:flex flex-col items-center justify-end h-full mt-20 gap-8 animate-float"
      style="animation-delay: 1s"
    >
      <!-- Bunch of Balloons -->
      <svg viewBox="0 0 100 150" class="w-24 h-32 drop-shadow-md pb-4">
        <!-- strings -->
        <path
          d="M 50 120 L 50 70 M 50 120 L 30 60 M 50 120 L 70 60"
          stroke="#cbd5e1"
          stroke-width="1.5"
          fill="none"
        />
        <!-- balloon 1 -->
        <ellipse cx="30" cy="40" rx="15" ry="20" fill="#fbcfe8" />
        <path d="M 28 60 L 32 60 L 30 63 Z" fill="#fbcfe8" />
        <!-- balloon 2 -->
        <ellipse cx="70" cy="45" rx="15" ry="18" fill="#fda4af" />
        <path d="M 68 63 L 72 63 L 70 66 Z" fill="#fda4af" />
        <!-- balloon 3 -->
        <ellipse cx="50" cy="25" rx="18" ry="22" fill="#ffccd5" />
        <path d="M 48 47 L 52 47 L 50 50 Z" fill="#ffccd5" />
        <!-- highlights -->
        <path
          d="M 25 30 Q 30 25 35 30"
          stroke="rgba(255,255,255,0.6)"
          stroke-width="2"
          fill="none"
          stroke-linecap="round"
        />
        <path
          d="M 65 35 Q 70 30 75 35"
          stroke="rgba(255,255,255,0.6)"
          stroke-width="2"
          fill="none"
          stroke-linecap="round"
        />
        <path
          d="M 45 15 Q 50 10 55 15"
          stroke="rgba(255,255,255,0.6)"
          stroke-width="2"
          fill="none"
          stroke-linecap="round"
        />
      </svg>

      <!-- New Sleeping Fluffy Cat -->
      <svg viewBox="0 0 100 80" class="w-32 h-24 drop-shadow-lg transform -rotate-6">
        <!-- fluffy body -->
        <path
          d="M 20 60 Q 15 40 40 40 Q 70 40 80 60 Q 80 75 50 75 Q 20 75 20 60 Z"
          fill="#B0B5B9"
        />
        <!-- curled tail -->
        <path
          d="M 80 60 Q 90 55 90 40 Q 90 20 70 20 Q 60 20 60 25"
          fill="none"
          stroke="#B0B5B9"
          stroke-width="12"
          stroke-linecap="round"
        />
        <!-- paw in front -->
        <ellipse cx="30" cy="70" rx="6" ry="4" fill="#a3a8ad" />
        <ellipse cx="45" cy="72" rx="6" ry="4" fill="#a3a8ad" />
        <!-- head resting on paws -->
        <circle cx="35" cy="55" r="18" fill="#a3a8ad" />
        <!-- ears -->
        <path d="M 20 45 L 15 30 L 30 40 Z" fill="#a3a8ad" />
        <path d="M 45 40 L 55 30 L 50 45 Z" fill="#a3a8ad" />
        <!-- internal pink ears -->
        <path d="M 21 43 L 18 34 L 28 39 Z" fill="#ffe4e8" />
        <path d="M 43 40 L 50 34 L 47 43 Z" fill="#ffe4e8" />
        <!-- sleepy eyes -->
        <path
          d="M 27 55 Q 31 58 34 55"
          fill="none"
          stroke="#2c3e50"
          stroke-width="1.5"
          stroke-linecap="round"
        />
        <path
          d="M 40 55 Q 44 58 47 55"
          fill="none"
          stroke="#2c3e50"
          stroke-width="1.5"
          stroke-linecap="round"
        />
        <!-- Zzz text -->
        <text
          x="20"
          y="25"
          fill="#FF9FB0"
          font-family="sans-serif"
          font-weight="bold"
          font-size="12"
          class="animate-pulse"
        >
          Z
        </text>
        <text
          x="10"
          y="15"
          fill="#FF9FB0"
          font-family="sans-serif"
          font-weight="bold"
          font-size="8"
          class="animate-pulse"
          style="animation-delay: 0.5s"
        >
          z
        </text>
      </svg>
    </div>

    <!-- CENTER FRONT: The Music Card -->
    <div class="flex flex-col items-center gap-6">
      <div
        class="w-full max-w-sm flex flex-col items-center gap-8 p-10 bg-white/70 backdrop-blur-md rounded-[3rem] shadow-2xl border border-white/50 animate-float relative z-10 transition-transform hover:scale-105 duration-500"
      >
        <!-- Soft blur background elements directly behind the player circle -->
        <div
          class="absolute top-0 right-0 w-32 h-32 bg-pink-soft rounded-full mix-blend-multiply opacity-50 blur-xl pointer-events-none"
        ></div>

        <div
          class="flex items-center gap-2 text-pink-400 font-bold tracking-widest text-sm bg-pink-50 px-4 py-1 rounded-full border border-pink-100 shadow-sm relative z-10"
        >
          <Volume2 :size="16" />
          <span class="font-sans">MUSIC BOX</span>
        </div>

        <!-- Vinyl Record Container -->
        <div
          class="relative w-56 h-56 flex items-center justify-center p-2 rounded-full border-4 border-slate-100 shadow-inner bg-slate-50 z-10"
        >
          <!-- Record Base -->
          <div
            class="w-full h-full rounded-full border-[6px] border-slate-800 bg-slate-800 shadow-xl overflow-hidden relative transition-transform duration-[20s] ease-linear"
            :class="{ 'animate-spin-slow': isPlaying }"
          >
            <!-- Grooves effect -->
            <div class="absolute inset-0 border-[10px] border-slate-700/50 rounded-full m-2"></div>
            <div class="absolute inset-0 border-[8px] border-slate-600/30 rounded-full m-5"></div>
            <div class="absolute inset-0 border-[6px] border-slate-500/20 rounded-full m-8"></div>

            <!-- Record Label (Cat Face) -->
            <div
              class="absolute inset-0 m-auto w-24 h-24 bg-pink-50 rounded-full border-[3px] border-pink-headband flex items-center justify-center shadow-inner overflow-hidden"
            >
              <img src="/public/pics/汐儿.png" />
            </div>
            <!-- Center hole -->
          </div>

          <!-- Tonearm decoration -->
          <div
            class="absolute top-2 -right-4 w-10 h-28 origin-top-right transition-transform duration-1000 ease-in-out pointer-events-none drop-shadow-lg z-20"
            :class="{ 'rotate-[25deg]': isPlaying, 'rotate-0': !isPlaying }"
          >
            <div
              class="w-3 h-3 bg-slate-300 rounded-full border border-slate-400 absolute top-0 -right-1.5"
            ></div>
            <div class="w-1.5 h-20 bg-slate-300 absolute top-1 right-0 rounded-b-full"></div>
            <div
              class="w-5 h-6 bg-pink-headband absolute bottom-0 -right-1.5 rounded shadow border border-pink-400"
            ></div>
          </div>
        </div>

        <div class="text-pink-400">🎵 Happy Birthday Song</div>

        <!-- Controls -->
        <button
          @click="togglePlay"
          class="flex items-center justify-center w-14 h-14 rounded-full bg-pink-400 text-white hover:bg-pink-500 active:scale-95 transition-all shadow-lg hover:shadow-pink-300 z-10"
        >
          <Pause v-if="isPlaying" fill="currentColor" stroke-width="0" :size="24" />
          <Play v-else fill="currentColor" stroke-width="0" :size="24" class="ml-1" />
        </button>

        <audio ref="audioRef" src="/PinkLetter/public/music.mp3" loop preload="auto"></audio>
      </div>

      <p
        class="text-slate-500 font-sans tracking-wide text-sm font-bold flex items-center justify-center gap-2"
      ></p>
    </div>

    <!-- RIGHT SIDE DECORATIONS & TEXT -->
    <div
      class="hidden md:flex flex-col items-start justify-center h-full mt-14 gap-8 animate-float"
      style="animation-delay: 0.5s"
    >
      <div class="flex items-end gap-2 lg:pl-6">
        <Heart
          fill="#ff9fb0"
          class="text-pink-100 drop-shadow-md w-10 h-10 transform rotate-12 mb-4"
        />

        <!-- Better Birthday Cake -->
        <svg viewBox="0 0 100 120" class="w-24 h-28 drop-shadow-lg transform -rotate-3">
          <!-- Plate -->
          <ellipse cx="50" cy="110" rx="48" ry="8" fill="#fff" stroke="#fff" stroke-width="2" />
          <!-- Cake Base -->
          <path d="M 15 105 L 15 65 Q 50 75 85 65 L 85 105 Q 50 115 15 105 Z" fill="#fff" />
          <!-- Bottom Frosting -->
          <ellipse cx="50" cy="105" rx="35" ry="5" fill="#fbcfe8" opacity="0.6" />
          <!-- Cake Top/Frosting -->
          <path
            d="M 12 65 Q 50 45 88 65 Q 92 80 85 85 Q 78 75 70 85 Q 60 75 50 85 Q 40 75 30 85 Q 22 75 15 85 Q 8 80 12 65 Z"
            fill="#FF9FB0"
          />
          <ellipse cx="50" cy="62" rx="38" ry="12" fill="#ff7da1" />
          <!-- Candles (3 candles) -->
          <rect x="30" y="35" width="4" height="20" fill="#cbd5e1" rx="2" />
          <rect x="48" y="25" width="4" height="25" fill="#cbd5e1" rx="2" />
          <rect x="66" y="35" width="4" height="20" fill="#cbd5e1" rx="2" />
          <!-- Flames -->
          <path d="M 32 20 Q 35 30 32 32 Q 29 30 32 20 Z" fill="#FFD700" class="animate-pulse" />
          <path
            d="M 50 10 Q 53 20 50 22 Q 47 20 50 10 Z"
            fill="#FFD700"
            class="animate-pulse"
            style="animation-delay: 0.3s"
          />
          <path
            d="M 68 20 Q 71 30 68 32 Q 65 30 68 20 Z"
            fill="#FFD700"
            class="animate-pulse"
            style="animation-delay: 0.6s"
          />
        </svg>
      </div>

      <!-- Description Card -->
      <div
        class="bg-white/80 backdrop-blur-sm p-6 rounded-2xl border border-white shadow-lg max-w-xs transition-transform hover:-translate-y-1 duration-300 relative ml-4"
      >
        <div
          class="absolute -top-3 -right-3 w-8 h-8 rounded-full bg-pink-100 flex items-center justify-center shadow-md border border-white"
        >
          <Heart class="text-pink-400" :size="14" fill="#ff9fb0" />
        </div>
        <h4 class="font-sans font-bold text-base text-slate-700 mb-2">尤克里里版 · 生日歌</h4>
        <p class="font-handwriting text-slate-500 text-lg leading-relaxed mb-4">
          我觉得一首普通的生日歌可能过于平淡，所以给你送上这个尤克里里的版本吧！它代表着轻快，明亮的节奏和哲学，希望你喜欢！
        </p>
        <p class="font-sans text-xs text-pink-400 tracking-wider">
          P.S.
          我本来想自己弹的，然后弹了两小时发现特喵的手太笨，而且录出来的声音太烂，所以换个大佬的给你听qwq...
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
.animate-spin-slow {
  animation: spin 6s linear infinite;
}
</style>
