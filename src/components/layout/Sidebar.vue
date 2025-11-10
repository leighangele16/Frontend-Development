<template>
  <div class="w-64 bg-white border-r border-gray-200 flex flex-col p-6 h-screen overflow-y-auto">
    <!-- Logo -->
    <div class="flex items-center gap-3 mb-8">
      <div class="w-40 h-40 bg-white rounded-full flex items-center justify-center flex-shrink-0 pl-4">
        <img
            src="/logo-name-nobg-1.png"
            alt="App Logo"
            class="w-40 h-40 object-contain"
          />
      </div>
      <div>
        <!-- <p class="font-bold text-xs leading-tight">ARCHIVER'S</p> -->
        <!-- <p class="font-bold text-xs leading-tight">VAULT</p> -->
      </div>
    </div>

    <!-- Navigation -->
    <nav class="space-y-2 flex-1">
      <NavItem icon="home" label="Home" :active="currentPage === 'home'" @click="$emit('navigate', 'home')" />
      <NavItem icon="search" label="Search" :active="currentPage === 'search'" @click="$emit('navigate', 'search')" />
      <NavItem icon="shelf" label="My Shelf" :active="currentPage === 'my-shelf'" @click="$emit('navigate', 'my-shelf')" />
      <NavItem icon="heart" label="Favorites" :active="currentPage === 'favorites'" @click="$emit('navigate', 'favorites')" />
    </nav>

    <!-- Footer -->
    <div class="space-y-2 pt-6 border-t border-gray-200">
      <p class="text-xs text-gray-500 px-4 mb-3">GENERAL</p>
      <NavItem icon="info" label="About" @click="$emit('navigate', 'about')" small />
      <NavItem icon="help" label="Support" @click="$emit('navigate', 'support')" small />
      <NavItem icon="terms" label="Terms & Condition" @click="$emit('navigate', 'terms')" small />
    </div>
  </div>
</template>

<script setup>
import NavItem from '../common/NavItem.vue'

defineProps({
  currentPage: String
})

defineEmits(['navigate', 'logout'])
</script>
