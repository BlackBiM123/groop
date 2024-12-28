<template>
  <div class="snow-field-container">
    <div class="snow-field">
      <div
        v-for="(snowflake, index) in snowflakes"
        :key="index"
        class="snowflake"
        :class="snowflake.type"
        :style="{
          left: `${snowflake.x}%`,
          width: `${snowflake.size}px`,
          height: `${snowflake.size}px`,
          opacity: snowflake.opacity,
          animationDuration: `${snowflake.fallDuration}s`,
          animationDelay: `${snowflake.delay}s`
        }"
      >
        <template v-if="snowflake.type === 'star'">
          <CustomIcon :name="snowflake.iconName" color="FFF"/>
        </template>
        <template v-else>
          <div class="circle"></div>
        </template>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useWindowSize } from '@vueuse/core'
import CustomIcon from './CustomIcon.vue';

const { width } = useWindowSize()
const snowflakes = ref([]);

// Массив возможных иконок
const iconNames = ['star', 'star-fill', 'star-half'];

const generateSnowflakes = (count) => {
  const generated = [];
  const columns = 20;
  const snowflakesPerColumn = Math.ceil(count / columns);
  
  for (let col = 0; col < columns; col++) {
    const columnStart = (col / columns) * 100;
    const columnWidth = 100 / columns;
    
    for (let i = 0; i < snowflakesPerColumn; i++) {
      const isSvg = Math.random() > 0.5;
      generated.push({
        type: isSvg ? "star" : "circle",
        iconName: iconNames[Math.floor(Math.random() * iconNames.length)],
        x: columnStart + (Math.random() * columnWidth * 0.8) + (columnWidth * 0.1),
        size: isSvg
          ? (width.value > 600 ? Math.random() * 12 + 8 : Math.random() * 8 + 6)
          : (Math.random() * 4 + 2),
        opacity: Math.random() * 0.7 + 0.3,
        fallDuration: 10 + Math.random() * 20,
        delay: -Math.random() * 20
      });
    }
  }
  
  snowflakes.value = generated.sort(() => Math.random() - 0.5);
};

onMounted(() => {
  generateSnowflakes(60);
});
</script>

<style scoped>
.snow-field-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 2;
}

.snow-field {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.snowflake {
  position: absolute;
  top: -20px;
  animation: snowfall linear infinite;
  will-change: transform;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}

.snowflake :deep(svg) {
  width: 100%;
  height: 100%;
}

.snowflake.circle {
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.8);
  box-shadow: 0 0 2px rgba(255, 255, 255, 0.3);
}

@keyframes snowfall {
  0% {
    transform: translate(0, 0) rotate(0deg);
  }
  25% {
    transform: translate(15px, 25vh) rotate(90deg);
  }
  50% {
    transform: translate(-15px, 50vh) rotate(180deg);
  }
  75% {
    transform: translate(15px, 75vh) rotate(270deg);
  }
  100% {
    transform: translate(-15px, 100vh) rotate(360deg);
  }
}
</style> 