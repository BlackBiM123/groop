<template>
  <div 
    class="custom-icon" 
    :style="{ 
      width: `${size}px`, 
      height: `${size}px`,
      color: `#${color}`
    }"
    v-html="svgContent"
  >
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  color: {
    type: String,
    default: '000'
  },
  size: {
    type: [Number, String],
    default: 24
  }
});

const svgContent = ref('');

const loadSvg = async () => {
  try {
    const response = await fetch(`/src/assets/images/svg/${props.name}.svg`);
    const svg = await response.text();
    svgContent.value = svg
      .replace('<svg', '<svg style="width: 100%; height: 100%;"')
      .replace(/fill="[^"]*"/g, `fill="#${props.color}"`); 
  } catch (error) {
    console.error(`Failed to load icon: ${props.name}`, error);
  }
};

onMounted(loadSvg);

watch(() => props.name, loadSvg);
</script>

<style scoped>
.custom-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;

  :deep(svg) {
    fill: currentColor;
  }
  path {
    fill: currentColor;
  }
}
</style> 
