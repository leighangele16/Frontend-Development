<template>
  <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
    <div class="bg-white rounded-lg max-w-md w-full p-8 space-y-6">
      <h2 class="text-2xl font-bold">Fill Up the Details</h2>

      <form @submit.prevent="handleBorrow" class="space-y-6">
        <!-- From Date -->
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-3">From</label>
          <div class="flex gap-3">
            <select v-model="borrowData.fromDay" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option value="">DD</option>
              <option v-for="i in 31" :key="i" :value="String(i).padStart(2, '0')">{{ String(i).padStart(2, '0') }}</option>
            </select>
            <select v-model="borrowData.fromMonth" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option value="">MM</option>
              <option v-for="i in 12" :key="i" :value="String(i).padStart(2, '0')">{{ String(i).padStart(2, '0') }}</option>
            </select>
            <select v-model="borrowData.fromYear" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option value="">YYYY</option>
              <option v-for="i in 5" :key="i" :value="2025 - i">{{ 2025 - i }}</option>
            </select>
          </div>
        </div>

        <!-- To Date -->
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-3">To</label>
          <div class="flex gap-3">
            <select v-model="borrowData.toDay" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option value="">DD</option>
              <option v-for="i in 31" :key="i" :value="String(i).padStart(2, '0')">{{ String(i).padStart(2, '0') }}</option>
            </select>
            <select v-model="borrowData.toMonth" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option value="">MM</option>
              <option v-for="i in 12" :key="i" :value="String(i).padStart(2, '0')">{{ String(i).padStart(2, '0') }}</option>
            </select>
            <select v-model="borrowData.toYear" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option value="">YYYY</option>
              <option v-for="i in 5" :key="i" :value="2025 - i">{{ 2025 - i }}</option>
            </select>
          </div>
        </div>

        <!-- Serial Number -->
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Book Serial No.</label>
          <input v-model="borrowData.serialNumber" type="text" placeholder="Enter 6 Digit Serial No. Or Scan" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" />
        </div>

        <!-- Description -->
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Description</label>
          <textarea v-model="borrowData.description" placeholder="Purpose" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" rows="3"></textarea>
        </div>

        <!-- Buttons -->
        <div class="flex gap-3 pt-4">
          <button @click="$emit('close')" type="button" class="flex-1 px-4 py-2 border border-gray-300 text-gray-700 rounded-lg font-medium hover:bg-gray-50 transition">
            Cancel
          </button>
          <button type="submit" class="flex-1 px-4 py-2 bg-black text-white rounded-lg font-medium hover:bg-gray-900 transition">
            BORROW
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  book: Object
})

const emit = defineEmits(['close', 'borrow'])

const borrowData = ref({
  fromDay: '',
  fromMonth: '',
  fromYear: '',
  toDay: '',
  toMonth: '',
  toYear: '',
  serialNumber: '',
  description: ''
})

const handleBorrow = () => {
  emit('borrow', borrowData.value)
}
</script>
