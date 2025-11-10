<template>
  <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
    <div class="bg-white rounded-lg max-w-md w-full p-8 space-y-6">
      <h2 class="text-2xl font-bold">Fill Up the Details</h2>

      <form @submit.prevent="handleReturn" class="space-y-6">
        <!-- From Date -->
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-3">From</label>
          <div class="flex gap-3">
            <select v-model="returnData.fromDay" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option>DD</option>
              <option v-for="i in 31" :key="i">{{ String(i).padStart(2, '0') }}</option>
            </select>
            <select v-model="returnData.fromMonth" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option>MM</option>
              <option v-for="i in 12" :key="i">{{ String(i).padStart(2, '0') }}</option>
            </select>
            <select v-model="returnData.fromYear" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option>YYYY</option>
              <option v-for="i in 5" :key="i">{{ 2025 - i }}</option>
            </select>
          </div>
        </div>

        <!-- To Date -->
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-3">To</label>
          <div class="flex gap-3">
            <select v-model="returnData.toDay" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option>DD</option>
              <option v-for="i in 31" :key="i">{{ String(i).padStart(2, '0') }}</option>
            </select>
            <select v-model="returnData.toMonth" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option>MM</option>
              <option v-for="i in 12" :key="i">{{ String(i).padStart(2, '0') }}</option>
            </select>
            <select v-model="returnData.toYear" class="flex-1 px-3 py-2 border border-gray-300 rounded-lg">
              <option>YYYY</option>
              <option v-for="i in 5" :key="i">{{ 2025 - i }}</option>
            </select>
          </div>
        </div>

        <!-- Serial Number -->
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Book Serial No.</label>
          <input v-model="returnData.serialNumber" type="text" placeholder="680E2023" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" />
        </div>

        <!-- Penalties -->
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Penalties</label>
          <input v-model="returnData.penalties" type="text" placeholder="₹100" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" />
        </div>

        <!-- Buttons -->
        <div class="flex flex-col gap-3 pt-4">
          <button type="submit" class="w-full px-4 py-2 bg-green-600 text-white rounded-lg font-medium hover:bg-green-700 transition">
            Pay Now
          </button>
          <button type="button" class="w-full px-4 py-2 bg-gray-600 text-white rounded-lg font-medium hover:bg-gray-700 transition">
            Credit
          </button>
          <button @click="$emit('close')" type="button" class="w-full px-4 py-2 border border-gray-300 text-gray-700 rounded-lg font-medium hover:bg-gray-50 transition">
            Cancel
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['close', 'return'])

const returnData = ref({
  fromDay: '',
  fromMonth: '',
  fromYear: '',
  toDay: '',
  toMonth: '',
  toYear: '',
  serialNumber: '',
  penalties: ''
})

const handleReturn = () => {
  emit('return', returnData.value)
}
</script>
