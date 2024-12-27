<template>
  <div class="star-field-container">
    <div class="star-field">
      <div
        v-for="(star, index) in stars"
        :key="index"
        class="star"
        :style="getStarStyle(star)"
      >
        <template v-if="star.type === 'svg'">
          <img src="@/assets/images/svg/star.svg" alt="star" />
        </template>
        <template v-else>
          <div class="circle"></div>
        </template>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import { useWindowSize } from '@vueuse/core'

const { width } = useWindowSize()
const stars = ref([]);
const mouseX = ref(0);
const mouseY = ref(0);

const generateStars = (count) => {
  const generatedStars = [];
  const columns = 7;
  const rows = 4;
  const cellWidth = 100 / columns;
  const cellHeight = 100 / rows;

  for (let row = 0; row < rows; row++) {
    for (let col = 0; col < columns; col++) {
      const baseX = col * cellWidth;
      const baseY = row * cellHeight;
      
      const offsetX = (Math.random() - 0.5) * cellWidth;
      const offsetY = (Math.random() - 0.5) * cellHeight;
      
      const isSvg = Math.random() > 0.5;
      generatedStars.push({
        type: isSvg ? "svg" : "circle",
        x: baseX + offsetX,         
        y: baseY + offsetY,        
        size: isSvg
          ? (width.value > 600 ? Math.random() * 1.5 + 0.1 : Math.random() * 0.5 + 0.1)
          : (Math.random() * 0.5 + 0.15),
        opacity: Math.random() * 0.5 + 0.5,
        rotation: Math.random() * 360,
        animationDelay: Math.random() * 5,
      });
    }
  }
  stars.value = generatedStars;
};

const handleMouseMove = (e) => {
  mouseX.value = (e.clientX / window.innerWidth - 0.5) * 2; 
  mouseY.value = (e.clientY / window.innerHeight - 0.5) * 2;
};


const getStarStyle = (star) => {
  const parallaxX = -mouseX.value * 20 * (star.size / 2); 
  const parallaxY = -mouseY.value * 20 * (star.size / 2);

  return {
    left: `calc(${star.x}% + ${parallaxX}px)`,
    top: `calc(${star.y}% + ${parallaxY}px)`,
    width: `${star.size}em`,
    height: `${star.size}em`,
    opacity: star.opacity,
    transform: `rotate(${star.rotation}deg)`,
    animationDelay: `${star.animationDelay}s`,
    transition: 'left 0.3s ease-out, top 0.3s ease-out', 
  };
};

onMounted(() => {
  generateStars(6);
  window.addEventListener('mousemove', handleMouseMove);
});

onUnmounted(() => {
  window.removeEventListener('mousemove', handleMouseMove);
});
</script>

<style scoped>
.star-field-container{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.star-field {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
  
}


.star {
  position: absolute;
  animation: twinkle 5s infinite; 
  will-change: transform; 
}


.circle {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background: white;
}


@keyframes twinkle {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.2;
  }
}
</style>
