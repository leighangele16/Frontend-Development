<template>
  <div class="space-y-8">
    <!-- Tabs -->
    <div class="border-b border-gray-200 flex gap-8 overflow-x-auto">
      <button v-for="tab in tabs" :key="tab" :class="['py-4 font-medium whitespace-nowrap border-b-2 transition', activeTab === tab ? 'text-gray-900 border-black' : 'text-gray-500 border-transparent']" @click="activeTab = tab">
        {{ tab }}
      </button>
    </div>

    <!-- Books Grid -->
    <div v-if="activeTab === 'All Books'" class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <div v-for="book in borrowedBooks" :key="book.id" class="bg-white rounded-lg overflow-hidden border border-gray-200 hover:shadow-lg transition">
        <img :src="book.cover" :alt="book.title" class="w-full h-40 object-cover" />
        <div class="p-4 space-y-2">
          <p class="font-medium text-gray-900 line-clamp-2">{{ book.title }}</p>
          <p class="text-sm text-gray-500">{{ book.author }}, {{ book.year }}</p>
          <div class="space-y-1 text-xs text-gray-600">
            <p>Borrowed on {{ book.borrowedDate }}</p>
            <p>Submission Due {{ book.dueDate }}</p>
          </div>
          <div class="flex gap-2 pt-2">
            <button @click="$emit('read', book)" class="flex-1 px-3 py-1 bg-green-600 text-white rounded-lg text-sm font-medium hover:bg-green-700 transition">
              Read
            </button>
            <button @click="$emit('return-book', book)" class="flex-1 px-3 py-1 bg-gray-200 text-gray-900 rounded-lg text-sm font-medium hover:bg-gray-300 transition">
              Return
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Favorite Books -->
    <div v-else-if="activeTab === 'Favourite'" class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <div v-for="book in borrowedBooks.filter(b => b.isFavorite)" :key="book.id" class="bg-white rounded-lg overflow-hidden border border-gray-200 hover:shadow-lg transition">
        <img :src="book.cover" :alt="book.title" class="w-full h-40 object-cover" />
        <div class="p-4">
          <p class="font-medium text-gray-900">{{ book.title }}</p>
        </div>
      </div>
    </div>

    <!-- Borrowed Books -->
    <div v-else-if="activeTab === 'Borrowed Books'" class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <div v-for="book in borrowedBooks" :key="book.id" class="bg-white rounded-lg overflow-hidden border border-gray-200 hover:shadow-lg transition">
        <img :src="book.cover" :alt="book.title" class="w-full h-40 object-cover" />
        <div class="p-4">
          <p class="font-medium text-gray-900">{{ book.title }}</p>
          <button @click="$emit('return-book', book)" class="w-full mt-2 px-3 py-1 bg-gray-200 text-gray-900 rounded-lg text-sm font-medium hover:bg-gray-300 transition">
            Return
          </button>
        </div>
      </div>
    </div>

    <!-- Notes & Bookmarks -->
    <div v-if="activeTab === 'All Books'" class="mt-12">
      <h3 class="text-2xl font-bold mb-6">Notes & Bookmarks</h3>
      <div class="grid grid-cols-4 gap-4">
        <div class="h-32 bg-orange-400 rounded-lg"></div>
        <div class="h-32 bg-pink-400 rounded-lg"></div>
        <div class="h-32 bg-green-400 rounded-lg"></div>
        <div class="h-32 bg-purple-600 rounded-lg"></div>
      </div>
    </div>

    <!-- Remainders -->
  <div class="bg-white rounded-lg p-6 shadow-sm">
    <h4 class="font-semibold text-gray-700 mb-4 font-bold">Remainders</h4>

    <div class="space-y-4">
      <div class="space-y-1">
        <p class="text-sm text-gray-800">
          Server Maintenance will be done on 16 Mar 2023 from 9AM to 10AM
        </p>
        <p class="text-xs font-semibold text-gray-600">IT Department</p>
        <p class="text-xs text-gray-400">Posted on 14 Mar 2023</p>
        <hr class="border-gray-200 mt-2" />
      </div>

      <div class="space-y-1">
        <p class="text-sm text-gray-800">
          Server Maintenance will be done on 16 Mar 2023 from 9AM to 10AM
        </p>
        <p class="text-xs font-semibold text-gray-600">IT Department</p>
        <p class="text-xs text-gray-400">Posted on 14 Mar 2023</p>
        <hr class="border-gray-200 mt-2" />
      </div>

      <div class="space-y-1">
        <p class="text-sm text-gray-800">
          Server Maintenance will be done on 16 Mar 2023 from 9AM to 10AM
        </p>
        <p class="text-xs font-semibold text-gray-600">IT Department</p>
        <p class="text-xs text-gray-400">Posted on 14 Mar 2023</p>
      </div>
    </div>
  </div>

  <!-- Pending Books -->
  <div class="bg-white rounded-lg p-6 shadow-sm">
    <h4 class="font-semibold text-gray-700 mb-4">Pending Books</h4>

    <div class="space-y-4">
      <div class="flex items-start gap-4">
        <img src="/book2.png" alt="Book" class="w-12 h-16 object-cover rounded" />
        <div class="flex-1">
          <p class="text-sm font-medium text-gray-900">The Design of EveryDay Things</p>
          <p class="text-xs text-gray-500">Don Norman, 1988</p>
          <p class="text-xs text-red-500 mt-1">13 Mar 2023 (Over Due)</p>
        </div>
        <button class="px-3 py-1 border border-gray-900 rounded text-sm text-gray-900">Return</button>
      </div>

      <div class="flex items-start gap-4">
        <img src="/book3.jpg" alt="Book" class="w-12 h-16 object-cover rounded" />
        <div class="flex-1">
          <p class="text-sm font-medium text-gray-900">Rich Dad Poor Dad</p>
          <p class="text-xs text-gray-500">Robert T. Kiyosaki, 1997</p>
          <p class="text-xs text-red-500 mt-1">13 Mar 2023 (Over Due)</p>
        </div>
        <button class="px-3 py-1 border border-gray-900 rounded text-sm text-gray-900">Return</button>
      </div>
    </div>
  </div>

  <!-- Requested Books -->
  <div class="bg-white rounded-lg p-6 shadow-sm">
    <h4 class="font-semibold text-gray-700 mb-4">Requested Books</h4>

    <div class="space-y-4">
      <div class="flex items-start gap-4">
        <img src="/book2.png" alt="Book" class="w-12 h-16 object-cover rounded" />
        <div class="flex-1">
          <p class="text-sm font-medium text-gray-900">The Great Gatsby</p>
          <p class="text-xs text-gray-500">F. Scott Fitzgerald</p>
          <p class="text-xs text-gray-400 mt-1">Expected by 15 Mar 2026</p>
        </div>
        <button class="px-3 py-1 bg-gray-400 text-white rounded text-sm cursor-not-allowed">Not Yet Available</button>
      </div>

      <div class="flex items-start gap-4">
        <img src="/book11.jpg" alt="Book" class="w-12 h-16 object-cover rounded" />
        <div class="flex-1">
          <p class="text-sm font-medium text-gray-900">Pride and Prejudice</p>
          <p class="text-xs text-gray-500">Jane Austen</p>
          <p class="text-xs text-gray-400 mt-1">Returned From User</p>
        </div>
        <button class="px-3 py-1 bg-green-500 text-white rounded text-sm">Available Now</button>
      </div>
    </div>
  </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'




defineProps({
  borrowedBooks: Array
})

defineEmits(['return-book', 'read'])

const tabs = ['All Books', 'Favourite', 'Borrowed Books', 'E-Books', 'Audio Books', 'Articles & Journals']
const activeTab = ref('All Books')
</script>
