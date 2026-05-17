<script setup lang="ts">
import { ref } from 'vue'
import GiftBox from './components/GiftBox.vue'
import MusicPlayer from './components/MusicPlayer.vue'
import LetterContent from './components/LetterContent.vue'
import ConfettiBackground from './components/ConfettiBackground.vue'
import PhotoWall from './components/PhotoWall.vue'

const currentStage = ref<'gift' | 'revealed'>('gift')
const musicPlayerRef = ref<InstanceType<typeof MusicPlayer> | null>(null)

const handleGiftOpen = () => {
  currentStage.value = 'revealed'
  // 打开礼物盒后自动播放音乐
  setTimeout(() => {
    musicPlayerRef.value?.playMusic()
  }, 2500)
}
</script>

<template>
  <main
    class="min-h-screen relative overflow-x-hidden font-sans text-slate-800 selection:bg-pink-soft selection:text-pink-500"
  >
    <!-- Confetti Background (V2 enhancement) -->
    <ConfettiBackground />

    <!-- Decorative Hanging Lights -->
    <div class="fixed top-0 left-6 md:left-20 z-20 pointer-events-none fade-in-down">
      <div class="w-[3px] h-24 md:h-40 bg-slate-700/60 mx-auto shadow-sm"></div>
      <div
        class="w-10 h-10 rounded-full bg-[#fff4cc] shadow-[0_0_40px_20px_rgba(255,223,130,0.7)] animate-pulse border-2 border-yellow-200 flex items-center justify-center mx-auto transform -translate-y-1"
      >
        <div class="w-4 h-4 bg-white rounded-full opacity-80 blur-[2px]"></div>
      </div>
    </div>
    <div
      class="fixed top-0 right-6 md:right-20 z-20 pointer-events-none fade-in-down"
      style="animation-delay: 0.3s"
    >
      <div class="w-[3px] h-32 md:h-56 bg-slate-700/60 mx-auto shadow-sm"></div>
      <div
        class="w-12 h-12 rounded-full bg-[#fff4cc] shadow-[0_0_50px_25px_rgba(255,223,130,0.7)] animate-pulse border-2 border-yellow-200 flex items-center justify-center mx-auto transform -translate-y-1"
        style="animation-delay: 0.3s"
      >
        <div class="w-5 h-5 bg-white rounded-full opacity-80 blur-[2px]"></div>
      </div>
    </div>

    <!-- Floating background decorative elements -->
    <div class="fixed inset-0 pointer-events-none opacity-60 z-0">
      <div
        class="absolute top-1/4 left-10 w-64 h-64 bg-pink-soft rounded-full mix-blend-multiply filter blur-3xl animate-float"
      ></div>
      <div
        class="absolute bottom-1/4 right-10 w-96 h-96 bg-cat-gray-light rounded-full mix-blend-multiply filter blur-3xl animate-float"
        style="animation-delay: 2s"
      ></div>
      <div
        class="absolute top-1/2 left-1/3 w-48 h-48 bg-pink-100 rounded-full mix-blend-multiply filter blur-3xl animate-float"
        style="animation-delay: 4s"
      ></div>
    </div>

    <!-- Main Content Stage -->
    <div class="relative z-10 w-full min-h-screen">
      <Transition name="fade" mode="out-in">
        <GiftBox v-if="currentStage === 'gift'" @opened="handleGiftOpen" />

        <div v-else class="w-full flex flex-col items-center py-20 gap-24">
          <!-- The Music Player (anchors the top after opening) -->
          <section class="min-h-[60vh] flex flex-col items-center justify-center fade-in-up">
            <MusicPlayer ref="musicPlayerRef" />
            <p
              class="mt-8 text-slate-400 font-sans tracking-widest text-sm uppercase animate-pulse"
            >
              Scroll Down
            </p>
          </section>

          <section class="w-full fade-in-up-delay">
            <PhotoWall />
          </section>

          <section class="w-full fade-in-up-delay mt-10">
            <LetterContent />
          </section>
        </div>
      </Transition>
    </div>
  </main>
</template>

<style scoped>
.fade-in-down {
  animation: fadeInDown 1.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translateY(-40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition:
    opacity 1.5s cubic-bezier(0.4, 0, 0.2, 1),
    transform 1.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(40px) scale(0.95);
}

.fade-leave-to {
  opacity: 0;
  transform: scale(1.1);
}

.fade-in-up {
  animation: fadeInUp 1.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(40px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in-up-delay {
  animation: fadeInUp 1.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
  animation-delay: 0.5s;
  opacity: 0;
}
</style>
