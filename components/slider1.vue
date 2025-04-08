<script setup>
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide, Navigation } from "vue3-carousel";

const slides = [
  {
    id: 1,
    name: "The Food Spot",
    image: "/2.jpg",
    rating: 5.0,
    reviews: 1,
    distance: "1.1km",
    categories: ["American", "Middle Eastern"],
  },
  {
    id: 2,
    name: "Taco Haven",
    image: "/download.jpg",
    rating: 4.8,
    reviews: 3,
    distance: "2.5km",
    categories: ["Mexican", "Fast Food"],
  },
  {
    id: 3,
    name: "Pasta Palace",
    image: "/4.jpg",
    rating: 4.5,
    reviews: 5,
    distance: "3.0km",
    categories: ["Italian", "Pasta"],
  },
  {
    id: 4,
    name: "Lahore Grill",
    image: "/4.jpg",
    rating: 4.5,
    reviews: 11,
    distance: "3.0km",
    categories: ["Pakistani", "Lahore"],
  },
];

const carouselConfig = {
  height: 400,
  itemsToShow: 2,
  wrapAround: true,
};
</script>

<template>
  <Carousel v-bind="carouselConfig">
    <Slide v-for="slide in slides" :key="slide.id" class="card">
      <div class="card-body">
        <img
          :src="slide.image"
          alt="image"
          style="width: 100%; height: 250px; border-radius: 10px"
        />

        <!-- Place Name -->
        <h3 style="text-align: left; font-size: 18px; font-weight: bold">
          {{ slide.name }}
        </h3>

        <!-- Ratings and Distance -->
        <div
          style="
            display: flex;
            justify-content: space-between;
            width: 100%;
            padding: 15px;
          "
        >
          <span style="font-size: 18px; color: gold; font-weight: bold">
            ★
            <span style="color: black; font-size: 12px; font-weight: 400">
              {{ slide.rating }}
            </span>
            <span style="font-size: 12px">
              💬 <span style="color: black">{{ slide.reviews }}</span>
            </span>
          </span>
          <span>
            <span style="font-size: 12px; font-weight: 400">
              📍───📍 <span>{{ slide.distance }}</span>
            </span>
          </span>
        </div>

        <!-- Category Labels -->
        <div
          style="
            display: flex;
            justify-content: space-between;
            gap: 10px;
            align-items: center;
            padding: 10px 0;
          "
        >
          <p
            v-for="category in slide.categories"
            :key="category"
            style="
              border: 2px solid green;
              padding: 5px 15px;
              border-radius: 10px;
              margin: 0;
              text-align: center;
              font-size: 14px;
              font-weight: bold;
            "
          >
            {{ category }}
          </p>
        </div>
      </div>
    </Slide>

    <template #addons>
      <Navigation />
    </template>
  </Carousel>
</template>
