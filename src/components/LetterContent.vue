<script setup lang="ts">
</script>

<template>
  <section
    class="w-full max-w-4xl mx-auto px-6 font-sans relative z-10 flex flex-col items-center justify-center gap-16">
    <!-- Letter Paper -->
    <div
      class="w-full bg-white/90 backdrop-blur-md rounded-lg shadow-2xl p-8 md:p-14 relative overflow-hidden text-slate-700">
      <!-- Tape decorations -->
      <div
        class="absolute -top-4 left-1/2 transform -translate-x-1/2 w-32 h-8 bg-white/40 shadow-sm border border-white/50 backdrop-blur-lg rotate-1 flex items-center justify-center opacity-70 border-dashed">
      </div>

      <!-- Lined paper effect -->
      <div class="absolute inset-0 pointer-events-none opacity-[0.04]" style="
          background-image: repeating-linear-gradient(
            transparent,
            transparent 35px,
            #ff9fb0 35px,
            #ff9fb0 36px
          );
        "></div>

      <!-- Letter Content -->
      <div
        class="relative z-10 font-sans font-bold text-base md:text-lg leading-[2.5rem] md:leading-[3rem] tracking-wide text-[#8a8f94]">
        <p class="mb-4 selection:bg-pink-100 font-bold text-pink-400">亲爱的贝塔，</p>

        <p class="mb-3 selection:bg-pink-100 indent-8">
          祝你22岁生日快乐！hiahia没想到吧每年生日我都能整新活。这是一封来自赛博的信，希望你能喜欢~
        </p>

        <p class="mb-3 selection:bg-pink-100 indent-8">
          首先，不要忘记给自己过一个有仪式感的生日~把你的巧克力备好哦！既然我不在场就劳烦那个小兔兔帮你一起切蛋糕，吃巧克力，许愿啦！上面还有很多以前的照片，虽然本来还准备了更多的，就这么稍微挑出来了几个有代表性的呢。不知道你回忆起了多少呢？哎呦我草现在回过头看你以前怎么这么淫荡啊（bushi
        </p>

        <p class="mb-3 selection:bg-pink-100 indent-8">
          咳咳，无论怎么样，在生日那天一定要好好照顾好自己，让自己开开心心的度过一天。你马上要开启新的征程，而我们近年确实也开始变的越来越忙，不过无论后面怎么样，也许那份教你编程，或者和你一起备战软考的时候，希望那份能量能带你继续走完今后的路程。身在何方都不要忘记，继续加油！
        </p>

        <p class="mt-6 text-right selection:bg-pink-100 pr-8 border-t border-dashed border-pink-200/50 pt-6">
          永远关心着的，<br />
          <span class="text-cyan-600 font-bold">钦灵~ 🐾</span>
        </p>
      </div>
    </div>
  </section>
</template>
