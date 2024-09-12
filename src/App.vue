<template>
  <div id="app">
    <!-- Click Counter -->
    <div class="box counter">
      <p>Pilih Angka: <span class="count">{{ count }}</span></p>
      <button @click="incrementCount" class="btn">Ketik Aku</button>
    </div>

    <!-- Background Color Changer -->
    <div class="box color-changer" :style="{ backgroundColor: bgColor }">
      <p class="changer-text">Change Background Color</p>
      <button @click="changeColor" class="btn">Change Color</button>
    </div>

    <!-- Image Carousel -->
    <div class="box carousel">
      <transition name="carousel-fade" mode="out-in">
        <img :src="images[currentImage]" alt="carousel image" class="carousel-image" :key="currentImage"/>
      </transition>
      <div class="carousel-controls">
        <button @click="prevImage" class="carousel-btn">Previous</button>
        <button @click="nextImage" class="carousel-btn">Next</button>
      </div>
    </div>
  </div>
</template>
<script>
import { ref } from 'vue';
import image1 from './assets/stowberry.jpg';
import image2 from './assets/strowberry 2.jpg';
import image3 from './assets/strowberry 3.jpg';
import image4 from './assets/strowberry 4.jpg';
import image5 from './assets/strowberry 5.jpg';

export default {
  name: 'App',
  setup() {
    const count = ref(0);
    const bgColor = ref('#ffebee'); // Light strawberry red background color for default
    const currentImage = ref(0);
    const images = [image1, image2, image3, image4, image5];
    const colors = ['#e57373', '#ef9a9a', '#f44336', '#c62828']; // Strawberry reds

    function incrementCount() {
      count.value++;
    }

    function changeColor() {
      const randomIndex = Math.floor(Math.random() * colors.length);
      bgColor.value = colors[randomIndex];
    }

    function prevImage() {
      currentImage.value = (currentImage.value + images.length - 1) % images.length;
    }

    function nextImage() {
      currentImage.value = (currentImage.value + 1) % images.length;
    }

    return {
      count,
      bgColor,
      currentImage,
      images,
      incrementCount,
      changeColor,
      prevImage,
      nextImage
    };
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333;
  margin-top: 60px;
  background-color: #e45656; /* Deep red background for the app */
}

.box {
  margin: 20px auto;
  padding: 20px;
  border-radius: 10px;
  border: 2px solid #d09292; /* Light strawberry red border */
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  background-color: #f8bbd0; /* Light pink background for boxes */
  max-width: 600px;
}

.counter, .color-changer, .carousel {
  margin-bottom: 40px;
}

.count {
  font-size: 1.5rem;
  font-weight: bold;
  color: #e57373; /* Light strawberry red text */
}

.changer-text {
  font-size: 1.2rem;
  font-weight: 500;
  color: #e57373; /* Light strawberry red text */
}

.btn {
  background-color: #e57373; /* Strawberry red button */
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

.btn:hover {
  background-color: #c62828; /* Darker strawberry red on hover */
}

.carousel {
  position: relative;
}

.carousel-image {
  width: 100%;
  height: auto;
  border-radius: 10px;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.carousel-image:hover {
  transform: scale(1.05);
}

.carousel-controls {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.carousel-btn {
  background-color: #e57373; /* Strawberry red button */
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1rem;
  margin: 0 10px;
  transition: background-color 0.3s ease;
}

.carousel-btn:hover { 
  background-color: #c62828; /* Darker strawberry red on hover */
}

.carousel-fade-enter-active, .carousel-fade-leave-active {
  transition: opacity 0.5s;
}

.carousel-fade-enter, .carousel-fade-leave-to /* .carousel-fade-leave-active in <2.1.8 */ {
  opacity: 0;
}
</style>
