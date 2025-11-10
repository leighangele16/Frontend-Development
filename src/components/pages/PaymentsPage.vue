<template>
  <div class="space-y-6">
    <h1 class="text-3xl font-bold">Payments & Penalties</h1>

    <!-- Penalties -->
    <div class="bg-white rounded-lg overflow-hidden shadow-sm border border-gray-200">
      <div class="p-6 border-b border-gray-200">
        <h2 class="text-xl font-bold">Outstanding Penalties</h2>
      </div>

      <table class="w-full" v-if="penalties.length > 0">
        <thead class="bg-gray-50 border-b border-gray-200">
          <tr>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Book Title</th>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Amount</th>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Reason</th>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="penalty in penalties" :key="penalty.id" class="border-b border-gray-200 hover:bg-gray-50">
            <td class="px-6 py-4 text-sm text-gray-900">{{ penalty.bookTitle }}</td>
            <td class="px-6 py-4 text-sm font-semibold text-red-600">₹{{ penalty.amount }}</td>
            <td class="px-6 py-4 text-sm text-gray-600">{{ penalty.reason }}</td>
            <td class="px-6 py-4">
              <button class="px-4 py-1 bg-green-600 text-white rounded-lg text-sm font-medium hover:bg-green-700 transition">
                Pay Now
              </button>
            </td>
          </tr>
        </tbody>
      </table>

      <div v-else class="p-6 text-center text-gray-600">
        <p>No pending penalties</p>
      </div>
    </div>

    <!-- Total Due -->
    <div class="bg-green-50 border border-green-200 rounded-lg p-6">
      <div class="flex items-center justify-between">
        <div>
          <p class="text-gray-600 mb-1">Total Amount Due</p>
          <p class="text-4xl font-bold text-green-700">₹{{ totalDue }}</p>
        </div>
        <button class="px-6 py-3 bg-green-600 text-white rounded-lg font-medium hover:bg-green-700 transition">
          Pay All Penalties
        </button>
      </div>
    </div>

    <!-- Payment Methods -->
    <div class="bg-white rounded-lg p-6 border border-gray-200">
      <h3 class="text-xl font-bold mb-4">Payment Methods</h3>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <button class="p-4 border border-gray-300 rounded-lg hover:border-black transition text-left">
          <p class="font-semibold">Credit/Debit Card</p>
          <p class="text-sm text-gray-600">Pay directly with card</p>
        </button>
        <button class="p-4 border border-gray-300 rounded-lg hover:border-black transition text-left">
          <p class="font-semibold">UPI/Digital Wallet</p>
          <p class="text-sm text-gray-600">Quick payment option</p>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  penalties: Array
})

const totalDue = computed(() => {
  return props.penalties?.reduce((sum, p) => sum + p.amount, 0) || 0
})
</script>
