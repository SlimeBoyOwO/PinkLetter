<script setup lang="ts">
import { ref } from 'vue'
import { Lock, Unlock, KeyRound, Sparkles } from 'lucide-vue-next'
import GreetingCard from './GreetingCard.vue'

const password = ref('')
const isUnlocked = ref(false)
const errorMsg = ref('')

const checkPassword = () => {
  if (password.value === '233') {
    isUnlocked.value = true
    errorMsg.value = ''
  } else {
    errorMsg.value = '密码错误，再算算喵~'
    setTimeout(() => (errorMsg.value = ''), 3000)
    // Shake animation
    const container = document.getElementById('puzzle-input-container')
    if (container) {
      container.classList.add('animate-shake')
      setTimeout(() => container.classList.remove('animate-shake'), 500)
    }
  }
}
</script>

<template>
  <div
    class="w-full max-w-7xl mx-auto my-8 transition-all duration-1000 ease-out"
    :class="[isUnlocked ? 'px-2 md:px-0' : 'px-4']"
  >
    <!-- IF NOT UNLOCKED -->
    <div
      v-if="!isUnlocked"
      class="w-full max-w-2xl mx-auto p-10 bg-white/90 backdrop-blur-md rounded-[2.5rem] shadow-xl border border-pink-100 flex flex-col items-center relative overflow-hidden"
    >
      <!-- Lock Header -->
      <div
        class="w-16 h-16 rounded-full bg-pink-100 flex items-center justify-center text-pink-400 mb-6 shadow-inner border border-pink-200"
      >
        <Lock :size="28" />
      </div>

      <div class="flex flex-col items-center text-center z-10">
        <h3 class="text-3xl font-bold font-sans text-slate-700 mb-4 tracking-wider">
          一个小谜题捏
        </h3>
        <p class="font-sans text-slate-500 mb-8 max-w-md leading-relaxed">
          一直灰色的小喵喵要爬上一个
          <span class="font-bold text-pink-400">12层</span> 的巨大生日蛋糕。<br />
          它每次跳跃只能向上跨 <span class="font-bold text-pink-400">1层或2层</span>。 <br /><br />
          请问，喵喵到达最顶层，一共有多少种不同的跳法呢？<br />
          <span class="text-xs text-slate-400">（完成解密以解锁生日贺卡）</span>
        </p>

        <div
          id="puzzle-input-container"
          class="flex flex-col items-center gap-4 w-full max-w-[16rem] transition-transform"
        >
          <div class="relative w-full">
            <input
              v-model="password"
              type="text"
              placeholder="输入答案..."
              class="w-full px-5 py-3 pl-12 rounded-full border border-slate-200 shadow-inner focus:outline-none focus:border-pink-300 focus:ring-4 focus:ring-pink-50 transition-all font-sans text-center text-lg text-slate-600 bg-white"
              @keyup.enter="checkPassword"
            />
            <KeyRound
              class="absolute left-4 top-1/2 transform -translate-y-1/2 text-slate-400"
              :size="20"
            />
          </div>

          <button
            @click="checkPassword"
            class="w-full py-3.5 bg-[#FF9FB0] text-white font-bold tracking-widest rounded-full shadow-lg shadow-[#FF9FB0]/40 hover:bg-[#ff7da1] hover:shadow-xl hover:-translate-y-0.5 active:translate-y-0 transition-all font-sans"
          >
            开启贺卡
          </button>
          <p
            v-if="errorMsg"
            class="h-4 text-sm font-sans text-red-500 mt-1 transition-opacity font-bold"
          >
            {{ errorMsg }}
          </p>
        </div>
      </div>
    </div>

    <!-- IF UNLOCKED: COMBINED LAYOUT -->
    <div
      v-else
      class="w-full flex flex-col xl:flex-row items-stretch justify-center gap-8 xl:gap-10 animate-fadeInUp"
    >
      <!-- PUZZLE SUCCESS INFO (Left) -->
      <div
        class="w-full xl:w-1/3 bg-white/95 p-10 rounded-[2.5rem] shadow-xl border border-green-100 flex flex-col items-center justify-center text-center relative overflow-hidden group"
      >
        <div class="absolute inset-0 bg-gradient-to-b from-green-50/50 to-pink-50/50 z-0"></div>

        <Sparkles
          class="text-yellow-400 absolute top-8 right-8 animate-spin-veryslow"
          :size="32"
          stroke-width="1.5"
        />
        <Sparkles
          class="text-pink-300 absolute bottom-12 left-10 animate-spin-veryslow"
          :size="24"
          style="animation-direction: reverse"
        />

        <div
          class="w-20 h-20 rounded-full bg-green-100 flex items-center justify-center text-green-500 mb-8 shadow-inner border border-green-200 relative z-10 transition-transform group-hover:scale-110 duration-500"
        >
          <Unlock :size="36" />
        </div>

        <h3 class="text-3xl font-bold font-sans text-slate-700 mb-6 relative z-10">密码正确！</h3>

        <p class="font-handwriting text-3xl leading-[3rem] text-[#FF9FB0] relative z-10 mb-4 px-2">
          好耶~ 其实...<br />
          无论前路有多少种走法，<br />
          无论你中间遇到了什么<br />
          都希望你都能开心地、<br />
          自由地<br />
          跃向你的下一站风景。
        </p>
      </div>

      <!-- GREETING CARD (Right) -->
      <div class="w-full xl:w-2/3 flex animate-fadeIn delay-300">
        <GreetingCard />
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes shake {
  0%,
  100% {
    transform: translateX(0);
  }
  25% {
    transform: translateX(-10px);
  }
  50% {
    transform: translateX(10px);
  }
  75% {
    transform: translateX(-10px);
  }
}
.animate-shake {
  animation: shake 0.4s ease-in-out;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px) scale(0.98);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}
.animate-fadeInUp {
  animation: fadeInUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
.animate-fadeIn {
  animation: fadeIn 1s ease-out forwards;
}

.animate-spin-veryslow {
  animation: spin 10s linear infinite;
}
</style>
