<template>
  <header
    class="bg-white border-b border-gray-200 px-8 py-4 flex items-center justify-between"
  >
    <div class="flex items-center gap-6 flex-1">
      <select
        class="px-3 py-2 border border-gray-300 rounded-lg text-sm font-medium"
      >
        <option>All</option>
      </select>
      <div class="flex-1 max-w-md">
        <input
          type="text"
          placeholder="Search"
          class="w-full px-4 py-2 border border-gray-300 rounded-lg text-sm"
        />
      </div>
      <!-- <button class="p-2 hover:bg-gray-100 rounded-lg transition">
        <svg
          class="w-5 h-5 text-gray-600"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M12 5v.01M12 12v.01M12 19v.01M12 6a1 1 0 110-2 1 1 0 010 2zm0 7a1 1 0 110-2 1 1 0 010 2zm0 7a1 1 0 110-2 1 1 0 010 2z"
          />
        </svg>
      </button> -->
    </div>

    <div class="flex items-center gap-4 pr-12">
      <select class="px-3 py-2 border border-gray-300 rounded-lg text-sm">
        <option>Lang</option>
      </select>
      <div
        class="border border-gray-300 rounded-lg py-2 text-gray-600 text-sm px-12 flex items-center justify-between"
      >
        <!-- Time -->
        <div class="flex items-center space-x-1">
          <img
            src="/icons/clock-line-icon.svg"
            alt="Clock Icon"
            class="w-3 h-3"
          />
          <span>09:00 HRS</span>
        </div>
        <!-- Date -->
        <div class="flex items-center space-x-1 pl-4">
          <img
            src="/icons/calendar-blank-icon.svg"
            alt="Calendar Icon"
            class="w-3 h-3"
          />
          <span>04-MARCH-2025</span>
        </div>
      </div>

      <div
        class="flex items-center space-x-2 text-sm text-black text-bold pr-12 bg-warning"
      >
        <!-- Profile Button (Left) -->
        <button
          @click="$emit('profile')"
          class="w-8 h-8 rounded-full bg-blue-500 flex items-center justify-center text-white text-xs font-bold"
        >
          {{ userName?.charAt(0) || "L" }}
        </button>

        <!-- Name (Right) -->
        <span class="font-medium">{{ userName || "Leigh" }}</span>
      </div>
    </div>
  </header>
</template>

<script setup>
defineProps({
  userName: String,
});

defineEmits(["profile"]);
</script>
