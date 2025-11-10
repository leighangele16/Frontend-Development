<template>
  <div class="bg-white text-gray-900 min-h-screen font-sans">
    <!-- Loading Page -->
    <LoadingPage
      v-if="currentPage === 'loading'"
      @complete="currentPage = 'login'"
    />

    <!-- Auth Pages -->
    <LoginPage
      v-else-if="currentPage === 'login'"
      @login="handleLogin"
      @register="currentPage = 'register'"
    />
    <RegisterPage
      v-else-if="currentPage === 'register'"
      @navigate-to-login="currentPage = 'login'"
      @register="handleRegister"
    />

    <!-- Main App -->
    <template v-else>
      <div class="flex h-screen bg-gray-50">
        <!-- Sidebar -->
        <Sidebar
          :current-page="currentPage"
          @navigate="currentPage = $event"
          @logout="handleLogout"
        />

        <!-- Main Content -->
        <div class="flex-1 overflow-auto flex flex-col">
          <!-- Header -->
          <Header :user-name="user.name" @profile="currentPage = 'profile'" />

          <!-- Pages -->
          <div class="flex-1 overflow-auto">
            <div class="p-6 md:p-8 max-w-7xl mx-auto">
              <HomePage
                v-if="currentPage === 'home'"
                :books="books"
                @select-book="selectBook"
              />
              <BookDetailPage
                v-else-if="currentPage === 'book-detail'"
                :book="selectedBook"
                @borrow="showBorrowModal = true"
                @read="currentPage = 'read'"
                @back="currentPage = 'home'"
              />
              <ReadPage
                v-else-if="currentPage === 'read'"
                :book="selectedBook"
                @back="currentPage = 'book-detail'"
              />
              <SearchPage
                v-else-if="currentPage === 'search'"
                :books="books"
                @select-book="selectBook"
              />
              <MyShelfPage
                v-else-if="currentPage === 'my-shelf'"
                :borrowed-books="borrowedBooks"
                @return-book="openReturnModal"
                @read="readBook"
              />
              <FavoritesPage
                v-else-if="currentPage === 'favorites'"
                :favorite-books="favoriteBooks"
                @select-book="selectBook"
              />
              <ProfilePage
                v-else-if="currentPage === 'profile'"
                :user="user"
                @update="updateUser"
              />
              <PaymentsPage
                v-else-if="currentPage === 'payments'"
                :penalties="penalties"
              />
            </div>
          </div>
        </div>
      </div>

      <!-- Borrow Modal -->
      <BorrowModal
        v-if="showBorrowModal"
        :book="selectedBook"
        @close="showBorrowModal = false"
        @borrow="handleBorrow"
      />

      <!-- Return Modal -->
      <ReturnModal
        v-if="showReturnModal"
        :book="bookToReturn"
        @close="showReturnModal = false"
        @return="handleReturn"
      />
    </template>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import LoadingPage from "./components/pages/LoadingPage.vue";
import LoginPage from "./components/pages/LoginPage.vue";
import RegisterPage from "./components/pages/RegisterPage.vue";
import Sidebar from "./components/layout/Sidebar.vue";
import Header from "./components/layout/Header.vue";
import HomePage from "./components/pages/HomePage.vue";
import BookDetailPage from "./components/pages/BookDetailPage.vue";
import ReadPage from "./components/pages/ReadPage.vue";
import SearchPage from "./components/pages/SearchPage.vue";
import MyShelfPage from "./components/pages/MyShelfPage.vue";
import FavoritesPage from "./components/pages/FavoritesPage.vue";
import ProfilePage from "./components/pages/ProfilePage.vue";
import PaymentsPage from "./components/pages/PaymentsPage.vue";
import BorrowModal from "./components/modals/BorrowModal.vue";
import ReturnModal from "./components/modals/ReturnModal.vue";

const currentPage = ref("loading");
const selectedBook = ref(null);
const bookToReturn = ref(null);
const showBorrowModal = ref(false);
const showReturnModal = ref(false);

const user = ref({
  name: "Leigh Alsula",
  email: "leigh@college.com",
  profilePicture: "https://api.dicebear.com/7.x/avataaars/svg?seed=Leigh",
  readings: 120,
  contributions: 10,
  registerNumber: "6022020",
  phone: "+91 9952508995",
  bio: "I am a Student",
});

const books = ref([
  {
    id: 1,
    title: "Don't Make Me Think",
    author: "Steve Krug",
    year: 2000,
    cover: "book1.jpg",
    rating: 5.0,
    ratings: 350,
    category: "Computer Science",
    availability: ["Hard Copy", "E-Book", "Audio book"],
    status: "In-Shelf",
    location: "CS A-15",
    isFavorite: true,
  },
  {
    id: 2,
    title: "The Design of Everyday Things",
    author: "Don Norman",
    year: 1988,
    cover: "book2.png",
    rating: 4.5,
    ratings: 280,
    category: "UX Design",
    availability: ["Hard Copy", "E-Book"],
    status: "Borrowed",
    location: "CS B-20",
  },
  {
    id: 3,
    title: "Rich Dad Poor Dad",
    author: "Robert T. Kiyosaki",
    year: 1997,
    cover: "book3.jpg",
    rating: 4.5,
    ratings: 450,
    category: "Financial MGMT",
    availability: ["Hard Copy", "E-Book", "Audio book"],
    status: "In-Shelf",
    location: "CS A-15",
    isFavorite: true,
  },
  {
    id: 4,
    title: "Lean UX",
    author: "Jeff Gothelf",
    year: 2016,
    cover: "book4.jpg",
    rating: 4.2,
    ratings: 200,
    category: "Design",
    availability: ["E-Book", "Audio book"],
    status: "In-Shelf",
    location: "DESIGN-10",
  },
  {
    id: 5,
    title: "The Road to React",
    author: "Steve Krug",
    year: 2020,
    cover: "book5.jpg",
    rating: 4.8,
    ratings: 320,
    category: "Programming",
    availability: ["Hard Copy", "E-Book"],
    status: "In-Shelf",
    location: "PROG-05",
  },
]);

const borrowedBooks = ref([
  {
    ...books.value[0],
    borrowedDate: "11 Mar 2023 09:00 AM",
    dueDate: "14 Mar 2023",
    type: "Hard Copy",
    status: "Borrowed",
  },
  {
    ...books.value[1],
    borrowedDate: "2 Mar 2023 09:00 AM",
    dueDate: "13 Mar 2023 (Over Due)",
    type: "E-Book",
    status: "Borrowed",
  },
]);

const favoriteBooks = ref(books.value.filter((b) => b.isFavorite));

const penalties = ref([
  {
    id: 1,
    bookTitle: "Don't Make Me Think",
    amount: 100,
    reason: "Late Return",
  },
]);

const handleLogin = (credentials) => {
  currentPage.value = "home";
};

const handleRegister = (data) => {
  currentPage.value = "home";
};

const handleLogout = () => {
  currentPage.value = "login";
};

const selectBook = (book) => {
  selectedBook.value = book;
  currentPage.value = "book-detail";
};

const readBook = (book) => {
  selectedBook.value = book;
  currentPage.value = "read";
};

const handleBorrow = (borrowData) => {
  borrowedBooks.value.push(selectedBook.value);
  showBorrowModal.value = false;
};

const openReturnModal = (book) => {
  bookToReturn.value = book;
  showReturnModal.value = true;
};

const handleReturn = (returnData) => {
  borrowedBooks.value = borrowedBooks.value.filter(
    (b) => b.id !== bookToReturn.value.id
  );
  showReturnModal.value = false;
};

const updateUser = (updatedData) => {
  user.value = { ...user.value, ...updatedData };
};

onMounted(() => {
  // change page after 800ms (adjust as needed)
  setTimeout(() => {
    currentPage.value = "login";
  }, 800);
});
</script>

<style>
/* Put component-specific CSS here only (or leave empty) */
</style>
