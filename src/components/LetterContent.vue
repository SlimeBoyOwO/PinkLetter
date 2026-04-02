<script setup lang="ts">
import { Camera, Paperclip } from 'lucide-vue-next'
</script>

<template>
  <section
    class="w-full max-w-7xl mx-auto px-6 font-sans relative z-10 flex flex-col md:flex-row items-start justify-center gap-16 md:gap-20"
  >
    <!-- LEFT SIDE: Letter Paper -->
    <div
      class="w-full md:w-[60%] bg-white/90 backdrop-blur-md rounded-lg shadow-2xl p-8 md:p-14 relative overflow-hidden text-slate-700"
    >
      <!-- Tape decorations -->
      <div
        class="absolute -top-4 left-1/2 transform -translate-x-1/2 w-32 h-8 bg-white/40 shadow-sm border border-white/50 backdrop-blur-lg rotate-1 flex items-center justify-center opacity-70 border-dashed"
      ></div>

      <!-- Lined paper effect -->
      <div
        class="absolute inset-0 pointer-events-none opacity-[0.04]"
        style="
          background-image: repeating-linear-gradient(
            transparent,
            transparent 35px,
            #ff9fb0 35px,
            #ff9fb0 36px
          );
        "
      ></div>

      <!-- Letter Content -->
      <div
        class="relative z-10 font-sans font-bold text-base md:text-lg leading-[2.5rem] md:leading-[3rem] tracking-wide text-[#8a8f94]"
      >
        <p class="mb-4 selection:bg-pink-100 font-bold text-pink-400">亲爱的梦凌汐，</p>

        <p class="mb-3 selection:bg-pink-100 indent-8">
          祝你生日快乐！我们真的已经为彼此庆祝过了很多次生日呢。虽然我也很感慨时间的流逝就是了...已经匆匆过去了四五年了，从高中到大学再到如今这样优秀的你，真的很辛苦了哦。
        </p>

        <p class="mb-3 selection:bg-pink-100 indent-8">
          首先还是要抱歉一下...？基于我是个废物社恐的关系，我一直没试过在学校寄过快递。取而代之的反而是一堆奇奇怪怪的东西。希望你收到了之后不要被吓出心脏病就是了（嘻嘻）。但总之如果那些东西能让你压力大的时候，照着看看自己感觉开心，我觉得这就是它最大的价值了？关于那个小蛋糕...
          最近你说你心情不好也不太想说的话，有时候千言万语抵不过一点甜品的慰藉。虽然知道你减肥，但希望你心情不好的时候可以享受一下甜品的多巴胺，然后继续加油面对生活吧！
        </p>

        <p class="mb-3 selection:bg-pink-100 indent-8">
          现在我们各自在自己的道路上走的越来越远，虽然没有往日的那般联系和烟火，但我相信也许这样默默的陪伴本身也是一种互通的语言。如今我更像是在海畔边看着远航的你，时不时感到感慨和欣慰呢。即便如此，也不要忘记自己征服大海、诗和远方的决心！
        </p>

        <p
          class="mt-6 text-right selection:bg-pink-100 pr-8 border-t border-dashed border-pink-200/50 pt-6"
        >
          永远关心着的，<br />
          <span class="text-cyan-600 font-bold">钦灵~ 🐾</span>
        </p>
      </div>
    </div>

    <!-- RIGHT SIDE: Polaroid Gallery Hanging logically -->
    <div class="w-full md:w-[40%] flex flex-col items-center relative pt-10 pb-20">
      <!-- Hanging String -->
      <div
        class="absolute top-[-12%] left-[-20%] right-[-20%] h-32 border-b-2 border-slate-300 rounded-[50%] pointer-events-none z-0"
      ></div>

      <div class="flex flex-col items-center gap-16 relative z-10 w-full mt-4">
        <!-- Polaroid 1 -->
        <div
          class="relative transform -rotate-6 hover:rotate-0 hover:scale-105 hover:z-20 transition-all duration-300"
        >
          <div
            class="absolute -top-12 left-1/2 transform -translate-x-1/2 w-[2px] h-12 bg-slate-200"
          ></div>
          <Paperclip
            class="absolute -top-5 left-1/2 transform -translate-x-1/2 -rotate-12 text-slate-400 shadow-sm"
            :size="24"
            stroke-width="1.5"
          />

          <div
            class="bg-white p-3 pb-10 shadow-lg hover:shadow-2xl border border-slate-100 rounded w-48 group"
          >
            <div
              class="w-full aspect-square bg-slate-50 flex items-center justify-center overflow-hidden border border-slate-200 relative"
            >
              <img
                src="/public/pics/图1.png"
                alt="Memory"
                class="w-full h-full object-cover mix-blend-multiply opacity-95 group-hover:opacity-100 transition-opacity"
              />
              <Camera
                class="absolute text-white opacity-0 group-hover:opacity-60 drop-shadow-md"
                :size="32"
              />
            </div>
            <p
              class="font-handwriting text-center text-slate-500 text-xl absolute bottom-2 w-full left-0 tracking-widest bg-white/50 backdrop-blur-sm"
            >
              Happy Birthday!
            </p>
          </div>
        </div>

        <!-- Polaroid 2 -->
        <div
          class="relative transform rotate-3 hover:rotate-0 hover:scale-105 hover:z-20 transition-all duration-300 md:ml-24"
        >
          <div
            class="absolute -top-16 left-1/2 transform -translate-x-1/2 w-[2px] h-16 bg-slate-200"
          ></div>
          <Paperclip
            class="absolute -top-5 left-1/2 transform -translate-x-1/2 rotate-12 text-slate-400 shadow-sm"
            :size="24"
            stroke-width="1.5"
          />

          <div
            class="bg-white p-3 pb-10 shadow-lg hover:shadow-2xl border border-slate-100 rounded w-48 group"
          >
            <div
              class="w-full aspect-square bg-pink-50 flex items-center justify-center overflow-hidden border border-slate-200"
            >
              <img
                src="/public/pics/图2.png"
                alt="Memory"
                class="w-full h-full object-cover mix-blend-multiply opacity-95 group-hover:opacity-100 transition-opacity"
              />
            </div>
            <p
              class="font-handwriting text-center text-slate-500 text-xl absolute bottom-2 w-full left-0 tracking-widest bg-white/50 backdrop-blur-sm"
            >
              Make a wish!
            </p>
          </div>
        </div>

        <!-- Polaroid 3 -->
        <div
          class="relative transform -rotate-2 hover:rotate-0 hover:scale-105 hover:z-20 transition-all duration-300 md:-ml-10"
        >
          <div
            class="absolute -top-[5rem] left-1/2 transform -translate-x-1/2 w-[2px] h-[5rem] bg-slate-200"
          ></div>
          <Paperclip
            class="absolute -top-5 left-1/2 transform -translate-x-1/2 -rotate-6 text-slate-400 shadow-sm"
            :size="24"
            stroke-width="1.5"
          />

          <div
            class="bg-white p-3 pb-10 shadow-lg hover:shadow-2xl border border-slate-100 rounded w-48 group"
          >
            <div
              class="w-full aspect-square bg-slate-100 flex flex-col items-center justify-center overflow-hidden border border-slate-200 border-dashed relative"
            >
              <img
                src="/public/pics/fun.gif"
                alt="Memory"
                class="w-full h-full object-cover mix-blend-multiply opacity-95 group-hover:opacity-100 transition-opacity"
              />
              <div
                class="absolute inset-0 bg-[#FF9FB0]/10 opacity-0 group-hover:opacity-100 transition-opacity pointer-events-none"
              ></div>
            </div>
            <p
              class="font-handwriting text-center text-slate-500 text-xl absolute bottom-2 w-full left-0 tracking-widest bg-white/50 backdrop-blur-sm"
            >
              And Have Fun~!
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
