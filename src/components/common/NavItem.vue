<template>
  <button
    :class="[
      'w-full text-left px-4 py-2 rounded-lg flex items-center gap-3 transition',
      active ? 'bg-gray-100 text-gray-900' : 'text-gray-600 hover:bg-gray-50',
      small ? 'text-sm' : 'text-base',
    ]"
    @click="$emit('click')"
  >
    <img
      v-if="icon === 'home'"
      src="/icons/home-svgrepo-com.svg"
      alt="Home Icon"
      class="w-5 h-5"
    />

    <img
      v-else-if="icon === 'search'"
      src="/icons/search.svg"
      alt="Search Icon"
      class="w-5 h-5"
    />

    <img
      v-else-if="icon === 'shelf'"
      src="/icons/shelf-shelves-icon.svg"
      alt="Shelf Icon"
      class="w-5 h-5"
    />
    <img
      v-else-if="icon === 'heart'"
      src="/icons/heart-icon.svg"
      alt="Heart Icon"
      class="w-5 h-5"
    />


    
    <svg
      v-else-if="icon === 'info'"
      class="w-5 h-5"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
      />
    </svg>
    <svg
      v-else-if="icon === 'help'"
      class="w-5 h-5"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
      />
    </svg>
    <svg
      v-else-if="icon === 'terms'"
      class="w-5 h-5"
      fill="none"
      stroke="currentColor"
      viewBox="0 0 24 24"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
      />
    </svg>
    <span>{{ label }}</span>
  </button>
</template>

<script setup>
defineProps({
  icon: String,
  label: String,
  active: Boolean,
  small: Boolean,
});

defineEmits(["click"]);
</script>
