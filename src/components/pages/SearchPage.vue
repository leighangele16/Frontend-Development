<template>
  <div class="space-y-6">
    <!-- Search and Filter -->
    <div class="flex gap-4 items-center">
      <input type="text" placeholder="Search books..." class="flex-1 px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" />
      <select class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black">
        <option>All Categories</option>
        <option>Computer Science</option>
        <option>Design</option>
        <option>Finance</option>
      </select>
    </div>

    <!-- Results Table -->
    <div class="bg-white rounded-lg overflow-hidden shadow-sm border border-gray-200">
      <table class="w-full">
        <thead class="bg-gray-50 border-b border-gray-200">
          <tr>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Title</th>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Ratings</th>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Category</th>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Availability</th>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Status</th>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="book in books" :key="book.id" class="border-b border-gray-200 hover:bg-gray-50 transition">
            <td class="px-6 py-4">
              <div class="flex items-center gap-3">
                <img :src="book.cover" :alt="book.title" class="w-10 h-12 object-cover rounded" />
                <div>
                  <p class="font-medium text-gray-900">{{ book.title }}</p>
                  <p class="text-sm text-gray-500">{{ book.author }}, {{ book.year }}</p>
                </div>
              </div>
            </td>
            <td class="px-6 py-4 text-sm text-gray-600">{{ book.rating }}/5</td>
            <td class="px-6 py-4 text-sm text-gray-600">{{ book.category }}</td>
            <td class="px-6 py-4">
              <div class="space-y-1">
                <div v-for="item in book.availability" :key="item" class="flex items-center gap-2 text-xs text-gray-600">
                  <span class="w-1.5 h-1.5 bg-green-500 rounded-full"></span>
                  {{ item }}
                </div>
              </div>
            </td>
            <td class="px-6 py-4">
              <span :class="['px-3 py-1 rounded-full text-xs font-medium', book.status === 'In-Shelf' ? 'bg-green-100 text-green-700' : 'bg-gray-100 text-gray-700']">
                {{ book.status }}
              </span>
            </td>
            <td class="px-6 py-4">
              <button @click="$emit('select-book', book)" class="px-4 py-1 border border-gray-300 rounded-lg text-sm font-medium hover:bg-gray-50 transition">
                Preview
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
defineProps({
  books: Array
})

defineEmits(['select-book'])
</script>
