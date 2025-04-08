<script setup>
import "vue3-carousel/carousel.css";
import { Carousel, Slide, Navigation } from "vue3-carousel";

const images = [
  { id: 1, src: "/download.jpg", name: "Fast Food" },
  { id: 2, src: "/2.jpg", name: "Heart" },
  { id: 3, src: "/download.jpg", name: "Fast Food" },
  { id: 4, src: "/4.jpg", name: "pizza" },
  { id: 5, src: "/4.jpg", name: " chezpizza" },
];

const carouselConfig = {
  height: 200,
  itemsToShow: 3.5,
  wrapAround: true,
};
</script>

<template>
  <Carousel v-bind="carouselConfig">
    <Slide v-for="image in images" :key="image.id">
      <div style="text-align: center">
        <img
          :src="image.src"
          alt="image"
          style="width: 100%; border-radius: 5px"
        />
        <p style="margin-top: 5px; font-weight: bold">{{ image.name }}</p>
      </div>
    </Slide>

    <template #addons>
      <Navigation />
    </template>
  </Carousel>
</template>
