<template>
  <div
    class="w-full h-screen flex items-center justify-center bg-black text-white"
  >
    <div class="text-center">
      <div class="animate-spin mb-4">
        <!-- svg spinner -->
        <svg
          class="w-12 h-12 text-white"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
        >
          <circle
            cx="12"
            cy="12"
            r="10"
            stroke-width="4"
            stroke-opacity="0.15"
          ></circle>
          <path
            d="M22 12a10 10 0 00-10-10"
            stroke-width="4"
            stroke-linecap="round"
          ></path>
        </svg>
      </div>
      <p class="text-sm">Loading…</p>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from "vue";
import { ref } from "vue";

const visible = ref(true);

onMounted(() => {
  setTimeout(() => (visible.value = false), 80);
});
</script>

<style scoped>
/* optional styles */
</style>
