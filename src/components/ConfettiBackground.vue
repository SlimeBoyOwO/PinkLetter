<script setup lang="ts">
import { ref } from 'vue'

// 柔和的明亮色系调色板（粉、米、银灰、白、蜜桃）
const palette = ['#FF9FB0', '#FFE4E8', '#a3a8ad', '#ffffff', '#FFD1DC', '#fbcfe8', '#fdba74']

// 1. 生成星尘和星星 (60个，保持流畅)
const particles = ref(
  Array.from({ length: 60 }, (_, i) => {
    const isStar = Math.random() > 0.5 // 50% 概率是四角星，50% 是圆形星尘
    const sizeBase = isStar ? 8 + Math.random() * 12 : 3 + Math.random() * 5

    return {
      id: i,
      type: isStar ? 'star' : 'dust',
      left: Math.random() * 100,
      animationDuration: 15 + Math.random() * 25, // 15s - 40s 极其缓慢的漂浮
      animationDelay: -Math.random() * 40, // 随机错开时间线
      twinkleDuration: 3 + Math.random() * 4, // 闪烁周期
      twinkleDelay: -Math.random() * 5,
      color: palette[Math.floor(Math.random() * palette.length)]!,
      size: sizeBase,
      swayAmount: -40 + Math.random() * 80, // X轴漂移距离 (vw)
    }
  }),
)

// 2. 生成明亮系背景星云 (奶油色、淡粉色、珍珠白)
const nebulas = ref([
  { id: 1, color: '#FFF8E7', top: '5%', left: '15%', size: '45vw', delay: '0s' }, // 奶油米色
  { id: 2, color: '#FFE4E8', top: '45%', left: '60%', size: '55vw', delay: '-10s' }, // 柔和淡粉
  { id: 3, color: '#F8F9FA', top: '75%', left: '10%', size: '40vw', delay: '-5s' }, // 珍珠白
])

// 3. 生成流星 (3个)
const shootingStars = ref(
  Array.from({ length: 3 }, (_, i) => ({
    id: i,
    top: Math.random() * 60,
    delay: Math.random() * 12,
    duration: 2.5 + Math.random() * 2, // 划过速度
  })),
)
</script>

<template>
  <!-- 容器：去掉了深色背景，完全透明，可完美叠加在你的白色/米色主背景上 -->
  <div class="fixed inset-0 pointer-events-none z-[1] overflow-hidden">
    <!-- 1. 背景星云 (柔和的呼吸色块，增加画面氛围感) -->
    <div
      v-for="n in nebulas"
      :key="`nebula-${n.id}`"
      class="absolute rounded-full opacity-60 blur-[80px] nebula-breathe"
      :style="
        {
          top: n.top,
          left: n.left,
          width: n.size,
          height: n.size,
          backgroundColor: n.color,
          animationDelay: n.delay,
        } as any
      "
    ></div>

    <!-- 2. 星星与星尘 -->
    <div
      v-for="p in particles"
      :key="p.id"
      class="absolute cosmic-particle"
      :class="p.type"
      :style="
        {
          left: `${p.left}vw`,
          width: `${p.size}px`,
          height: `${p.size}px`,
          backgroundColor: p.color,
          /* 圆形星尘增加微弱的光晕 */
          boxShadow: p.type === 'dust' ? `0 0 ${p.size * 1.5}px ${p.color}` : 'none',
          /* 同时应用下落和闪烁动画 */
          animationDuration: `${p.animationDuration}s, ${p.twinkleDuration}s`,
          animationDelay: `${p.animationDelay}s, ${p.twinkleDelay}s`,
          '--sway-x': `${p.swayAmount}vw`,
        } as any
      "
    ></div>

    <!-- 3. 浅色系流星 -->
    <div
      v-for="s in shootingStars"
      :key="`shooting-${s.id}`"
      class="absolute shooting-star"
      :style="
        {
          top: `${s.top}vh`,
          animationDelay: `${s.delay}s`,
          animationDuration: `${s.duration}s`,
        } as any
      "
    ></div>
  </div>
</template>

<style scoped>
/* ====== 星星与星尘下落 & 漂移 ====== */
@keyframes cosmic-fall {
  0% {
    transform: translate3d(0, -10vh, 0) rotate(0deg);
  }
  100% {
    transform: translate3d(var(--sway-x), 110vh, 0) rotate(720deg);
  }
}

/* ====== 星星闪烁 (仅修改透明度，避免与下落的 transform 冲突) ====== */
@keyframes twinkle {
  0%,
  100% {
    opacity: 0.3;
  }
  50% {
    opacity: 1;
  }
}

.cosmic-particle {
  /* 组合下落和闪烁动画 */
  animation-name: cosmic-fall, twinkle;
  animation-timing-function: linear, ease-in-out;
  animation-iteration-count: infinite, infinite;
}

/* 圆形星尘 */
.cosmic-particle.dust {
  border-radius: 50%;
}

/* 四角星形状 (利用 clip-path 绘制星星) */
.cosmic-particle.star {
  clip-path: polygon(50% 0%, 60% 40%, 100% 50%, 60% 60%, 50% 100%, 40% 60%, 0% 50%, 40% 40%);
}

/* ====== 星云呼吸效果 ====== */
@keyframes nebula-breathe {
  0%,
  100% {
    transform: scale(1) translate(0, 0);
    opacity: 0.4;
  }
  50% {
    transform: scale(1.1) translate(2vw, 2vh);
    opacity: 0.7;
  }
}
.nebula-breathe {
  animation: nebula-breathe 15s ease-in-out infinite;
}

/* ====== 流星效果 (适配浅色背景) ====== */
@keyframes shooting-star-anim {
  0% {
    transform: translateX(120vw) translateY(-20vh) rotate(35deg);
    opacity: 1;
  }
  100% {
    transform: translateX(-20vw) translateY(80vh) rotate(35deg);
    opacity: 0;
  }
}

.shooting-star {
  width: 80px;
  height: 2px;
  /* 流星的渐变尾巴：从透明过渡到柔和的粉色 */
  background: linear-gradient(90deg, rgba(255, 159, 176, 0) 0%, #ff9fb0 100%);
  border-radius: 999px;
  right: 0;
  opacity: 0;
  animation: shooting-star-anim linear infinite;
  /* 流星头部的亮光 */
  box-shadow: 2px 0 6px #ff9fb0;
}
</style>
