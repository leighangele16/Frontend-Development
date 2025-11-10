<template>
  <div v-if="book" class="h-full bg-gray-900 rounded-lg overflow-hidden flex flex-col">
    <!-- Header -->
    <div class="bg-gray-800 px-6 py-4 flex items-center justify-between">
      <button @click="$emit('back')" class="flex items-center gap-2 text-white hover:text-gray-300 transition">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/></svg>
      </button>

      <div class="flex items-center gap-4">
        <div class="flex items-center gap-2">
          <img :src="book.cover" :alt="book.title" class="w-10 h-12 object-cover rounded" />
          <div class="text-white">
            <p class="font-semibold text-sm">{{ book.title }}</p>
            <p class="text-xs text-gray-400">{{ book.author }}</p>
          </div>
        </div>

        <div class="flex items-center gap-2">
          <button class="text-white hover:text-yellow-400 transition">
            <svg class="w-5 h-5 fill-current" viewBox="0 0 20 20"><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/></svg>
          </button>
          <button class="text-white hover:text-gray-300 transition">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"/></svg>
          </button>
        </div>

        <div class="flex items-center gap-4">
          <button class="px-4 py-2 border border-white text-white rounded-lg hover:bg-white hover:text-gray-900 transition">Full Screen</button>
          <select class="px-3 py-2 bg-gray-700 text-white rounded-lg border border-gray-600">
            <option>View</option>
          </select>
        </div>
      </div>
    </div>

    <!-- Content -->
    <div class="flex-1 flex items-center justify-center relative p-8 bg-white">
      <button @click="currentPage--" class="absolute left-4 text-gray-400 hover:text-gray-600 transition"
        v-if="currentPage > 1">
        <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/></svg>
      </button>

      <div class="max-w-2xl">
        <div class="text-sm font-semibold text-gray-600 mb-4 text-center">INTRODUCTION</div>
        <h2 class="text-4xl font-bold text-center mb-8">RICH DAD POOR DAD</h2>
        <p class="text-center text-gray-600 italic mb-8">Having two dads offered me the choice of contrasting points of view: one of a rich man and one of a poor man.</p>
        <div class="bg-gray-100 p-8 rounded-lg">
          <p class="text-gray-700 leading-relaxed">
            I had two fathers, a rich one and a poor one. One was highly educated and intelligent. He had a Ph.D. and completed four years of undergraduate work in less than two years. He then went on to Stanford University, the University of Chicago, and Northwestern University to do his advanced studies, all on full financial scholarship.
          </p>
        </div>
      </div>

      <button @click="currentPage++" class="absolute right-4 text-gray-400 hover:text-gray-600 transition">
        <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/></svg>
      </button>

      <div class="absolute bottom-4 right-4 text-sm text-gray-600">{{ currentPage }} & {{ currentPage + 1 }} of 200</div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  book: Object
})

defineEmits(['back'])

const currentPage = ref(1)
</script>
