<template>
  <div class="space-y-8">
    <!-- Today's Quote + Books Showcase -->
    <div
      class="flex flex-col lg:flex-row bg-white text-white rounded-xl overflow-hidden"
    >
      <!-- Quote Section (40%) -->
      <div class="w-full lg:w-2/5 p-8 flex flex-col justify-center bg-black">
        <h3 class="text-lg font-semibold mb-4">Today's Quote</h3>
        <transition name="fade" mode="out-in">
          <p key="quote.text" class="text-lg italic mb-4">
            {{ currentQuote.text }}
          </p>
        </transition>
        <div class="flex items-center gap-2">
          <div class="flex gap-1">
            <span
              v-for="(q, i) in quotes"
              :key="i"
              class="w-2 h-2 rounded-full"
              :class="i === currentIndex ? 'bg-white' : 'bg-gray-600'"
            ></span>
          </div>
          <p class="text-sm text-gray-400 ml-4">-{{ currentQuote.author }}</p>
        </div>
      </div>

      <!-- Books Section (60%) -->
      <div
        class="w-full lg:w-3/5 flex border-1 overflow-hidden pl-6"
      >
        <!-- Vertical label bar (10-15%) -->
        <div class="w-[12%] bg-black flex items-center justify-center">
          <span
            class="text-white font-bold transform -rotate-90 whitespace-nowrap"
          >
            NEW ARRIVALS
          </span>
        </div>

        <!-- Books Section (remaining 88%) -->
        <div
          class="w-[88%] p-8 bg-white flex items-center justify-center transition-all duration-500"
          @mouseenter="toggleBooks(true)"
          @mouseleave="toggleBooks(false)"
        >
          <transition name="fade-slide" mode="out-in">
            <div
              :key="showingAlt"
              class="grid grid-cols-3 gap-4 w-full max-w-3xl"
            >
              <div
                v-for="book in activeBooks"
                :key="book.id"
                class="cursor-pointer group"
              >
                <div
                  class="aspect-[3/4] bg-gray-700 rounded-lg overflow-hidden mb-2 group-hover:shadow-lg transform group-hover:-translate-y-2 transition duration-300"
                >
                  <img
                    :src="book.cover"
                    :alt="book.title"
                    class="w-full h-full object-cover"
                  />
                </div>
                <p class="text-sm font-medium text-black font-bold truncate">
                  {{ book.title }}
                </p>
                <p class="text-xs text-gray-800">{{ book.author }}</p>
              </div>
            </div>
          </transition>
        </div>
      </div>
    </div>

    <!-- New Arrivals -->
    <div>
      <h2 class="text-2xl font-bold">Good Morning</h2>
      <div class="flex items-center justify-between mb-4">
        <h3 class="text-2xl pt-5">New Arrivals</h3>
        <button class="text-gray-600 text-sm hover:text-gray-900">
          Show All
        </button>
      </div>
      <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-6 gap-4">
        <div
          v-for="book in books.slice(0, 6)"
          :key="book.id"
          @click="$emit('select-book', book)"
          class="cursor-pointer group"
        >
          <div
            class="aspect-[3/4] bg-gray-200 rounded-lg overflow-hidden mb-2 group-hover:shadow-lg transition transform group-hover:scale-105 duration-200"
          >
            <img
              :src="book.cover"
              :alt="book.title"
              class="w-full h-full object-cover"
            />
          </div>
          <p class="text-sm font-medium text-gray-900 truncate">
            {{ book.title }}
          </p>
          <p class="text-xs text-gray-500">{{ book.author }}</p>
        </div>
      </div>
    </div>

    <!-- Recommended Books -->
    <div>
      <div class="flex items-center justify-between mb-4">
        <h2 class="text-2xl">Recommended for You</h2>
        <button class="text-gray-600 text-sm hover:text-gray-900">
          Show All
        </button>
      </div>
      <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-6 gap-4">
        <div
          v-for="book in books"
          :key="book.id"
          @click="$emit('select-book', book)"
          class="cursor-pointer group"
        >
          <div
            class="aspect-[3/4] bg-gray-200 rounded-lg overflow-hidden mb-2 group-hover:shadow-lg transition transform group-hover:scale-105 duration-200"
          >
            <img
              :src="book.cover"
              :alt="book.title"
              class="w-full h-full object-cover"
            />
          </div>
          <p class="text-sm font-medium text-gray-900 truncate">
            {{ book.title }}
          </p>
          <p class="text-xs text-gray-500">{{ book.author }}</p>
        </div>
      </div>
    </div>

    <!-- Recent Readings -->
    <div>
      <div class="flex items-center justify-between mb-4">
        <h2 class="text-2xl">Recent Readings</h2>
        <button class="text-gray-600 text-sm hover:text-gray-900">
          Show All
        </button>
      </div>
      <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-6 gap-4">
        <div
          v-for="book in books"
          :key="book.id"
          @click="$emit('select-book', book)"
          class="cursor-pointer group"
        >
          <div
            class="aspect-[3/4] bg-gray-200 rounded-lg overflow-hidden mb-2 group-hover:shadow-lg transition transform group-hover:scale-105 duration-200"
          >
            <img
              :src="book.cover"
              :alt="book.title"
              class="w-full h-full object-cover"
            />
          </div>
          <p class="text-sm font-medium text-gray-900 truncate">
            {{ book.title }}
          </p>
          <p class="text-xs text-gray-500">{{ book.author }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from "vue";

defineProps({
  books: Array,
});

defineEmits(["select-book"]);

// === Quotes Rotation ===
const quotes = [
  {
    text: "There is more treasure in books than in all the pirate's loot on Treasure Island.",
    author: "Walt Disney",
  },
  {
    text: "A room without books is like a body without a soul.",
    author: "Marcus Tullius Cicero",
  },
  {
    text: "So many books, so little time.",
    author: "Frank Zappa",
  },
  {
    text: "Books are a uniquely portable magic.",
    author: "Stephen King",
  },
];

const currentIndex = ref(0);
const currentQuote = computed(() => quotes[currentIndex.value]);
const dotCount = computed(() => (currentIndex.value % 4) + 1);

let quoteInterval;
onMounted(() => {
  quoteInterval = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % quotes.length;
  }, 4000);
});
onBeforeUnmount(() => clearInterval(quoteInterval));

// === Books Showcase Swap ===
const booksSet1 = [
  {
    id: 1,
    title: "The Great Gatsby",
    author: "F. Scott Fitzgerald",
    cover: "/book6.jpg",
  },
  { id: 2, title: "1984", author: "George Orwell", cover: "/book7.jpg" },
  {
    id: 3,
    title: "To Kill a Mockingbird",
    author: "Harper Lee",
    cover: "/book8.jpg",
  },
];
const booksSet2 = [
  { id: 4, title: "Moby Dick", author: "Herman Melville", cover: "/book9.jpg" },
  {
    id: 5,
    title: "The Hobbit",
    author: "J.R.R. Tolkien",
    cover: "/book10.png",
  },
  {
    id: 6,
    title: "Pride and Prejudice",
    author: "Jane Austen",
    cover: "/book11.jpg",
  },
];

const showingAlt = ref(false);
const activeBooks = computed(() => (showingAlt.value ? booksSet2 : booksSet1));

let hoverTimeout = null;

function toggleBooks(state) {
  clearTimeout(hoverTimeout);

  if (state) {
    // Delay before switching to alternate set (500ms)
    hoverTimeout = setTimeout(() => {
      showingAlt.value = true;
    }, 2000);
  } else {
    // Delay before switching back (also 500ms for smoothness)
    hoverTimeout = setTimeout(() => {
      showingAlt.value = false;
    }, 2000);
  }
}
</script>
