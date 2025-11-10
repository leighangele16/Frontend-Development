<template>
  <div v-if="book" class="space-y-6">
    <!-- Header -->
    <button @click="$emit('back')" class="flex items-center gap-2 text-gray-600 hover:text-gray-900 transition">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/></svg>
      Back to results
    </button>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      <!-- Left: Book Cover and Actions -->
      <div class="md:col-span-1 space-y-4">
        <div class="w-full aspect-video bg-gray-200 rounded-lg overflow-hidden">
          <img :src="book.cover" :alt="book.title" class="w-full h-full object-cover" />
        </div>

        <div class="flex gap-2">
          <button class="flex-1 bg-black text-white py-2 rounded-lg font-medium hover:bg-gray-900 transition flex items-center justify-center gap-2">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 10l-2 1m0 0l-2-1m2 1v2.5M20 7l-2 1m2-1l-2-1m2 1v2.5M14 4l-2 1m0 0L10 4m2 1v2.5M2 7l2 1m-2-1l2-1m-2 1v2.5"/></svg>
            Notes
          </button>
          <button class="flex-1 bg-gray-200 text-gray-900 py-2 rounded-lg font-medium hover:bg-gray-300 transition flex items-center justify-center gap-2">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.684 13.342C9.922 10.938 11.539 9.5 13.5 9.5c1.961 0 3.578 1.438 4.816 3.842m-11.132 12.856c-1.632-2.526-2.324-5.084-2.324-7.792 0-5.468 4.251-9.5 9.5-9.5s9.5 4.032 9.5 9.5c0 2.708-.692 5.266-2.324 7.792M15 19H9m0 0l1.5-1.5m-1.5 1.5l-1.5-1.5"/></svg>
            Share
          </button>
        </div>

        <button @click="$emit('borrow')" class="w-full bg-black text-white py-2 rounded-lg font-medium hover:bg-gray-900 transition">
          BORROW
        </button>

        <button @click="$emit('read')" class="w-full bg-green-600 text-white py-2 rounded-lg font-medium hover:bg-green-700 transition flex items-center justify-center gap-2">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z"/></svg>
          Read Now
        </button>
      </div>

      <!-- Right: Book Details -->
      <div class="md:col-span-2 space-y-6">
        <div>
          <h1 class="text-3xl font-bold mb-2">{{ book.title }}</h1>
          <p class="text-gray-600">By <span class="font-medium">{{ book.author }}</span>, {{ book.year }}</p>
          <p class="text-sm text-gray-500 mt-1">Second Edition</p>
        </div>

        <!-- Rating -->
        <div class="flex items-center gap-4">
          <div class="flex items-center gap-1">
            <span v-for="i in 5" :key="i" class="text-yellow-400">★</span>
            <span class="text-sm text-gray-600 ml-2">{{ book.rating }}/5 Ratings</span>
          </div>
          <span class="text-sm text-gray-500">{{ book.ratings }} Currently reading</span>
          <span class="text-sm text-gray-500">119 Have read</span>
        </div>

        <!-- Availability -->
        <div class="bg-gray-50 p-4 rounded-lg">
          <h3 class="font-semibold mb-3">Availability</h3>
          <div class="flex flex-wrap gap-2">
            <span v-for="item in book.availability" :key="item" class="flex items-center gap-2 text-sm">
              <span class="w-2 h-2 bg-green-500 rounded-full"></span>
              {{ item }}
            </span>
          </div>
        </div>

        <!-- Status -->
        <div class="grid grid-cols-2 gap-4">
          <div class="bg-green-100 p-4 rounded-lg">
            <p class="text-sm text-gray-600">Status</p>
            <p class="text-lg font-bold text-green-700">{{ book.status }}</p>
          </div>
          <div class="bg-blue-100 p-4 rounded-lg">
            <p class="text-sm text-gray-600">Location</p>
            <p class="text-lg font-bold text-blue-700">{{ book.location }}</p>
          </div>
        </div>

        <!-- Tabs -->
        <div class="border-b border-gray-200">
          <div class="flex gap-8">
            <button class="py-4 font-medium text-gray-900 border-b-2 border-black">Overview</button>
            <button class="py-4 font-medium text-gray-500">Details</button>
            <button class="py-4 font-medium text-gray-500">Reviews</button>
          </div>
        </div>

        <!-- Overview -->
        <div class="space-y-4">
          <div>
            <h4 class="font-semibold mb-2">About Author</h4>
            <p class="text-gray-600 text-sm">{{ book.author }} is a renowned author with expertise in {{ book.category }}</p>
          </div>

          <div>
            <h4 class="font-semibold mb-3">Other Books</h4>
            <div class="flex gap-4">
              <div class="w-20 h-28 bg-gray-200 rounded-lg"></div>
              <div class="w-20 h-28 bg-gray-200 rounded-lg"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  book: Object
})

defineEmits(['back', 'borrow', 'read'])
</script>
