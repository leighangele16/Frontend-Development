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

    <!-- Login form -->
    <div
      class="relative z-10 bg-white rounded-2xl p-8 w-full max-w-md shadow-2xl"
    >
      <div class="flex flex-col items-center mb-8">
        <div
          class="w-50 h-50 bg-white rounded-full flex items-center justify-center mb-4"
        >
          <img
            src="/logo-name-nobg-1.png"
            alt="App Logo"
            class="w-50 h-50 object-contain"
          />
        </div>
        <!-- <h1 class="text-2xl font-bold text-center">ARCHIVER'S VAULT</h1> -->
        <h2 class="text-gray-600 mt-2">Welcome Back!</h2>
        <p class="text-gray-500 text-xs mt-1">
          Sign in to continue to your Digital Library
        </p>
      </div>

      <form @submit.prevent="handleLogin" class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2"
            >Email</label
          >
          <input
            v-model="email"
            type="email"
            placeholder="username@collegename.ac.in"
            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-2"
            >Password</label
          >
          <div class="relative">
            <input
              v-model="password"
              :type="showPassword ? 'text' : 'password'"
              placeholder="••••••••"
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-black"
            />
            <button
              @click="showPassword = !showPassword"
              type="button"
              class="absolute right-3 top-2.5 text-gray-600"
            >
              <svg
                class="w-5 h-5"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
                />
              </svg>
            </button>
          </div>
        </div>

        <div class="flex items-center justify-between">
          <label class="flex items-center gap-2">
            <input type="checkbox" class="w-4 h-4 rounded border-gray-300" />
            <span class="text-sm text-gray-700">Remember me</span>
          </label>
          <a href="#" class="text-sm text-gray-600 hover:text-gray-900"
            >Forgot password?</a
          >
        </div>

        <button
          type="submit"
          class="w-full bg-black text-white py-2 rounded-lg font-medium hover:bg-gray-900 transition mt-6"
        >
          Login
        </button>
      </form>

      <div class="mt-6 flex items-center justify-between text-sm pb-8">
        <span class="text-gray-600"
          >New User?
          <button
            @click="$emit('register')"
            class="text-gray-900 font-medium hover:underline"
          >
            Register Here
          </button></span
        >
        <button class="text-gray-600 font-medium hover:underline">
          Use as Guest
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const email = ref("user@collegename.ac.in");
const password = ref("password");
const showPassword = ref(false);

const emit = defineEmits(["login", "register"]);

const handleLogin = () => {
  emit("login", { email: email.value, password: password.value });
};
</script>
