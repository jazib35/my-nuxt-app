<template>
  <div class="card">
    <div class="p-1">
      <div class="card-body">
        <span style="font-size: 20px; font-weight: bold; text-align: left">
          {{ data.category }}
        </span>
        <br />
        {{ data.name }}
        <br />
        {{ data.decription }}
        <div class="img-container">
          <img :src="data.image_src" alt="images" class="img-cover" />
        </div>
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
            <span
              style="
                color: black;
                font-size: 10px;
                font-weight: 400;
                margin-right: 8px;
              "
            >
              {{ data.rating }}
            </span>
            <span style="font-size: 12px; margin-left: 8px">
              💬
              <span style="color: black; font-size: 10px; font-weight: 400">{{
                data.comment
              }}</span>
            </span>
          </span>

          <span>
            <span style="font-size: 10px; font-weight: 400">
              📍───📍
              <span style="font-size: 10px; font-weight: 400"
                >{{ data.distance }}km</span
              >
            </span>
          </span>
        </div>

        <div class="cousine_container">
          <p class="cousine_text" v-for="cuisine in data.cuisines">
            {{ cuisine }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const { data } = defineProps(["data"]);

console.log(data);
</script>

<style scoped>
.cousine_container {
  display: flex;
  gap: 10px;
  align-items: center;
  bottom: 15px;
}

.cousine_text {
  border: 2px solid green;
  width: 100px;
  border-radius: 10px;
  margin: 0;
  text-align: center;
}
.img-cover {
  width: 100%;
  height: 250px;
  border-radius: 5px;
  object-fit: cover;
  display: block; /* Prevents extra space below the image */
}
</style>
