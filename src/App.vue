<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const fullImage = ref('https://images.unsplash.com/photo-1615917018845-f705f7ec1388?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=978&q=80')

const images = [
  {
    thumb: "https://images.unsplash.com/photo-1615917018845-f705f7ec1388?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=978&q=80",
    full: "https://images.unsplash.com/photo-1615917018845-f705f7ec1388?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=978&q=80"
  },
  {
    thumb: "https://images.unsplash.com/photo-1559720092-98f763329fce?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80",
    full: "https://images.unsplash.com/photo-1559720092-98f763329fce?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80"
  },
  {
    thumb: "https://images.unsplash.com/photo-1612467968134-e58957756c7a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=871&q=80",
    full: "https://images.unsplash.com/photo-1612467968134-e58957756c7a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=871&q=80"
  },
  {
    thumb: "https://images.unsplash.com/photo-1621820932454-76e98d967237?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80",
    full: "https://images.unsplash.com/photo-1621820932454-76e98d967237?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80"
  }
];

const autoplayInterval = 3000; // Time interval between image changes (in milliseconds)
let autoplayTimer; // Variable to hold the autoplay timer

let currentIndex = ref(0); // Current index of the displayed image

// Function to set the current image
function setImage(image) {
  fullImage.value = image.full;
  currentIndex.value = images.indexOf(image);
}

// Function to handle autoplay
function startAutoplay() {
  autoplayTimer = setInterval(() => {
    const nextIndex = (currentIndex.value + 1) % images.length;
    setImage(images[nextIndex]);
  }, autoplayInterval);
}

// Function to stop autoplay
function stopAutoplay() {
  clearInterval(autoplayTimer);
}

// Start autoplay when the component is mounted
onMounted(() => {
  startAutoplay();
});

// Stop autoplay when the component is unmounted
onUnmounted(() => {
  stopAutoplay();
});

const arrowStyle = "bg-gray-500/75 p-3 rounded-lg text-white"

// Function to show the next image
function nextImage() {
  currentIndex.value = (currentIndex.value + 1) % images.length;
  fullImage.value = images[currentIndex.value].full;
}

// Function to show the previous image
function prevImage() {
  currentIndex.value = (currentIndex.value - 1 + images.length) % images.length;
  fullImage.value = images[currentIndex.value].full;
}
</script>

<template>
  <section class="bg-gradient-to-r from-red-300 to-yellow-300 h-screen">
    <div class="relative w-1/2 mx-auto flex items-center flex-col">
      <h1 class="text-center text-3xl uppercase text-white py-10">It's an awesome image carousel using Vue 3</h1>
      <div class="h-[350px] w-full">
        <img class="cursor-pointer w-full h-full rounded-lg" :src="fullImage">
      </div>

      <div class="mt-5">
        <div class="grid grid-cols-4 gap-3">
          <img class="cursor-pointer h-20 w-full border-4 rounded-md shadow-lg"
            @click="setImage(image)"
            v-for="image in images"
            :src="image.thumb"
            :key="image.thumb"
          >
        </div>
      </div>

      <!-- Navigation Buttons -->
      <div class="mt-4">
        <button @click="prevImage" :class="arrowStyle" class="absolute top-1/2 left-2">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5" />
          </svg>
        </button>
        
        <button @click="nextImage" :class="arrowStyle" class="absolute top-1/2 right-2">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
          </svg>
        </button>
      </div>
    </div>
  </section>
</template>

<style scoped>
</style>
