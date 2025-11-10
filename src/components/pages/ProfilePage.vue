<template>
  <div class="max-w-4xl space-y-6">
    <!-- Tabs -->
    <div class="border-b border-gray-200 flex gap-8">
      <button v-for="tab in tabs" :key="tab" :class="['py-4 font-medium border-b-2 transition', activeTab === tab ? 'text-gray-900 border-black' : 'text-gray-500 border-transparent']" @click="activeTab = tab">
        {{ tab }}
      </button>
    </div>

    <!-- Account Setting Tab -->
    <div v-if="activeTab === 'Account Setting'" class="bg-white rounded-lg p-8 border border-gray-200 space-y-6">
      <!-- Profile Picture and Stats -->
      <div class="flex items-center gap-8">
        <div class="w-32 h-32 bg-blue-500 rounded-full flex items-center justify-center text-white text-4xl font-bold">
          {{ user.name?.charAt(0) }}
        </div>
        <div class="space-y-4">
          <div class="flex gap-8">
            <div class="bg-black text-white px-6 py-4 rounded-lg text-center">
              <div class="text-2xl font-bold">{{ user.readings }}</div>
              <div class="text-sm">Readings</div>
            </div>
            <div class="bg-white border border-gray-300 px-6 py-4 rounded-lg text-center">
              <div class="text-2xl font-bold">{{ user.contributions }}</div>
              <div class="text-sm">Contribution</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Form -->
      <div class="grid grid-cols-2 gap-6">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Full name</label>
          <input v-model="formData.fullName" type="text" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" />
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">College Email ID</label>
          <input v-model="formData.email" type="email" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" />
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">Register Number</label>
          <input v-model="formData.registerNumber" type="text" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" />
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">phone number</label>
          <input v-model="formData.phone" type="tel" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" />
        </div>
      </div>

      <!-- Bio -->
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-2">Bio</label>
        <textarea v-model="formData.bio" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black" rows="4"></textarea>
      </div>

      <!-- Buttons -->
      <div class="flex gap-4">
        <button @click="saveProfile" class="px-6 py-2 bg-black text-white rounded-lg font-medium hover:bg-gray-900 transition">
          Update Profile
        </button>
        <button class="px-6 py-2 border border-gray-300 text-gray-700 rounded-lg font-medium hover:bg-gray-50 transition">
          Reset
        </button>
      </div>
    </div>

    <!-- Other Tabs -->
    <div v-else class="bg-white rounded-lg p-8 border border-gray-200">
      <p class="text-gray-600">{{ activeTab }} content coming soon...</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  user: Object
})

const emit = defineEmits(['update'])

const tabs = ['Account Setting', 'Login & Security', 'Notifications', 'Interface']
const activeTab = ref('Account Setting')

const formData = ref({
  fullName: props.user.name,
  email: props.user.email,
  registerNumber: props.user.registerNumber,
  phone: props.user.phone,
  bio: props.user.bio
})

const saveProfile = () => {
  emit('update', formData.value)
}
</script>
