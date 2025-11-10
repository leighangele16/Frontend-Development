<template>
  <div
    class="h-screen w-screen bg-gradient-to-br from-black via-gray-900 to-black flex items-center justify-center overflow-hidden p-4"
  >
    <!-- Background S -->
    <div class="absolute inset-0 overflow-hidden bg-black">
      <!-- Black wonky yin-yang-like curve with fade -->
      <svg
        class="absolute inset-0 w-full h-full"
        viewBox="0 0 1440 320"
        xmlns="http://www.w3.org/2000/svg"
        preserveAspectRatio="none"
      >
        <defs>
          <!-- black-to-transparent vertical fade -->
          <linearGradient id="fade-to-white" x1="1" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#ffffff" />
            <stop offset="70%" stop-color="#ffffff" stop-opacity="0.5" />
            <stop offset="100%" stop-color="#ffffff" stop-opacity="0" />
          </linearGradient>
        </defs>
        <!-- Curvy S-like shape -->
        <path
          fill="url(#fade-to-white)"
          d="M0,320 C200,240 400,80 720,160 C1040,240 1240,60 1440,0 L1440,320 L0,320 Z"
        />
      </svg>
    </div>

    <div
      class="relative z-10 bg-white rounded-2xl p-8 w-full max-w-md shadow-2xl"
    >
      <div class="flex flex-col items-center mb-8">
        <div
          class="w-50 h-50 bg-white rounded-full flex items-center justify-center mb-4"
        >
          <img src="/logo-name-nobg-1.png" alt="App Logo" class="w-50 h-50" />
        </div>
        <h1 class="text-2xl font-bold">Create Account</h1>
        <p class="text-gray-600 text-sm mt-2">Join Archiver's Vault</p>
      </div>

      <form @submit.prevent="handleRegister" class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2"
            >Full Name</label
          >
          <input
            v-model="fullName"
            type="text"
            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2"
            >Email</label
          >
          <input
            v-model="email"
            type="email"
            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2"
            >Password</label
          >
          <input
            v-model="password"
            type="password"
            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2"
            >College ID</label
          >
          <input
            v-model="collegeId"
            type="text"
            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
          />
        </div>

        <button
          type="submit"
          class="w-full bg-black text-white py-2 rounded-lg font-medium hover:bg-gray-900 transition mt-6"
        >
          Register
        </button>
      </form>

      <div class="mt-6 text-center text-sm">
        <span class="text-gray-600"
          >Already have an account?
          <button
            @click="$emit('navigate-to-login')"
            class="text-gray-900 font-medium hover:underline"
          > 
            Login
          </button></span
        >
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const fullName = ref("");
const email = ref("");
const password = ref("");
const collegeId = ref("");

const emit = defineEmits(["register", "login"]);

const handleRegister = () => {
  emit("register", {
    fullName: fullName.value,
    email: email.value,
    password: password.value,
    collegeId: collegeId.value,
  });
};
</script>
