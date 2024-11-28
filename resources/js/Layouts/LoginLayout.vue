<template>
  <div :class="theme">
    <div class="font-[sans-serif] min-h-screen flex flex-col items-center justify-center bg-cover bg-center" :style="{ backgroundImage: 'url(/images/pigbackground.png)' }">
      <div class="w-full sm:max-w-md mt-6 px-6 py-4 glass-effect shadow-md overflow-hidden sm:rounded-lg">
        <slot />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, defineProps } from 'vue';

const props = defineProps({
  theme: String,
  toggleTheme: Function,
});

onMounted(() => {
  if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
    props.theme.value = 'dark';
    document.documentElement.classList.add('dark');
  }
});
</script>

<style>
.glass-effect {
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
}
</style>