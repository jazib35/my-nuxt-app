<script setup>
import { ref } from "vue";

const rating = ref(0); // Initial rating
const emit = defineEmits(["update:rating"]);
// Function to update rating when clicking a star
const setRating = (value) => {
  rating.value = value;
  emit("update:rating", rating.value);
};
</script>

<template>
  <div>
    <div>
      <span
        v-for="star in 5"
        :key="star"
        @click="setRating(star)"
        style="cursor: pointer; font-size: 24px"
      >
        <span v-if="star <= rating" style="color: gold">★</span>
        <span v-else style="color: lightgray">★</span>
      </span>
    </div>
    <p>{{ rating }} / 5</p>
  </div>
</template>
