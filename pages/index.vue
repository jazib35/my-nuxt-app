<template>
  <div class="hadder">
    <nav class="navbar navbar-expand-lg">
      <div class="container-fluid">
        <div class="collapse navbar-collapse" id="navbarNav">
          <img src="/logo.svg" />
          <ul
            class="navbar-nav"
            style="display: flex; justify-content: center; width: 100%"
          >
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Features</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Pricing</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Disabled</a>
            </li>
          </ul>
          <div class="d-flex">
            <a class="btn btn-light me-2">Login</a>
            <a class="btn btn-success">Logout</a>
          </div>
        </div>
      </div>
    </nav>

    <p class="header-text">
      The original & world's largest guide to Halal restaurants & markets
    </p>

    <p
      style="
        font-size: 43px;
        font-weight: 700;
        text-align: center;
        color: white;
      "
    >
      SERVING <span style="color: yellow">HALAL FOODIES</span> FOR OVER 20 YEARS
    </p>

    <div
      class="row gx-1 justify-content-center"
      style="margin-left: 70px; margin-right: 70px"
    >
      <div class="col-12 col-md-5 mt-2 mt-md-0">
        <div class="p-1">
          <div class="container mt-3">
            <div class="input-group">
              <input
                type="text"
                id="locationInput"
                class="form-control"
                placeholder="Enter your location"
              />
            </div>
          </div>
        </div>
      </div>

      <div class="col-12 col-md-5 mt-2 mt-md-0">
        <div class="p-1">
          <div class="container mt-3">
            <div class="input-group">
              <input
                v-model="searchQuery"
                type="text"
                class="form-control"
                placeholder="Search for food..."
              />
            </div>
          </div>
        </div>
      </div>

      <div class="col-12 col-md-2 text-center text-md-start">
        <div class="p-1">
          <button
            type="button"
            class="btn btn-success"
            style="margin-top: 15px"
          >
            SEARCH
          </button>
        </div>
      </div>
    </div>

    <!-- Store Buttons -->
    <div
      class="store-buttons d-flex flex-wrap justify-content-center gap-3 mt-3"
    >
      <a href="https://www.apple.com/app-store/" target="_blank">
        <img
          src="https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg"
          alt="Download on the App Store"
          class="img-fluid store-badge"
        />
      </a>
      <a href="https://play.google.com/store" target="_blank">
        <img
          src="https://upload.wikimedia.org/wikipedia/commons/7/78/Google_Play_Store_badge_EN.svg"
          alt="Get it on Google Play"
          class="img-fluid store-badge"
        />
      </a>
    </div>
  </div>
  <div class="container mt-3">
    <!-- Search Input -->
    <input
      v-model="searchQuery"
      type="text"
      class="form-control"
      placeholder="Search for food..."
    />
  </div>

  <br />
  <div class="container overflow-hidden text-center">
    <div class="container">
      <div class="row gx-3">
        <!-- Sidebar (Full-width on small screens, 3 columns on medium & larger) -->
        <div class="col-12 col-md-3 p-3 text-center">
          <div class="p-3">
            <p
              style="
                font-size: 18px;
                font-weight: 600;
                line-height: 28px;
                text-align: left;
              "
            >
              Filter your results
            </p>
            <div class="d-flex justify-content-between">
              <span>Search radius</span>

              <span id="kmValue" class="font-bold">1km</span>
            </div>
            <input
              type="range"
              id="kmRange"
              class="form-range"
              min="1"
              max="32"
              step="1"
              v-model="distanceFilter"
              oninput="document.getElementById('kmValue').textContent = this.value"
            />
            KM

            <p
              class="my-3"
              style="
                font-size: 14px;
                font-weight: 600;
                line-height: 24px;
                text-align: left;
                color: rgb(54, 65, 82);
              "
            >
              Halal filters
            </p>
            <div class="form-check form-switch my-3">
              <label class="form-check-label" for="flexSwitchCheckChecked">
                <p
                  style="
                    font-size: 14px;
                    font-weight: 500;
                    line-height: 20px;
                    color: rgb(54, 65, 82);
                  "
                >
                  Show only fully halal places
                </p>
              </label>
              <input
                class="form-check-input"
                type="checkbox"
                role="switch"
                v-model="halalOnlyPlaces"
                id="flexSwitchCheckChecked"
              />
            </div>
            <div class="form-check form-switch my-3">
              <label class="form-check-label" for="flexSwitchCheckChecked">
                <p style="font-size: 14px; font-weight: 500; line-height: 20px">
                  Hide places that serve/allow alcohol
                </p>
              </label>
              <input
                class="form-check-input"
                type="checkbox"
                role="switch"
                id="flexSwitchCheckChecked"
                v-model="hideAlcoholPlaces"
              />
            </div>
            <p
              style="
                font-size: 14px;
                font-weight: 600;
                line-height: 24px;
                text-align: left;
              "
            >
              Show places with ratings above
            </p>
            <star @update:rating="handleRatingUpdate" />
          </div>
        </div>

        <!-- Main Content (Full-width on small screens, 9 columns on medium & larger) -->
        <div class="col-12 col-md-9">
          <div class="row">
            <div
              class="col-12 col-md-4 col-lg-4"
              v-for="place in filteredPlaces"
            >
              <place :data="place" />
            </div>
          </div>
          <!-- <div class="p-3">
            <p
              style="
                font-size: 24px;
                font-weight: 500;
                line-height: 29px;
                color: rgb(33, 37, 41);
                text-align: left;
              "
            >
              Featured near New York
            </p>
            <slider1 />
          </div>
          <p
            style="
              font-size: 24px;
              font-weight: 500;
              line-height: 27px;
              color: rgb(41, 41, 41);
              text-align: left;
            "
          >
            1630 halal places near New York
          </p>
          <slider2 /> -->
        </div>
      </div>
    </div>
    <hr />

    <fotter />
  </div>
</template>

<script setup>
import { Carousel, Slide, Pagination, Navigation } from "vue3-carousel";

import places from "~/assets/json/places.json";

const searchQuery = ref("");
const distanceFilter = ref("15");
const ratingFilter = ref("");
const halalOnlyPlaces = ref(false);
const hideAlcoholPlaces = ref(false);

const filteredPlaces = computed(() => {
  return places.filter((place) => {
    // Apply halal filter
    // if (filter.only_halal && !place.halal) return false;
    if (halalOnlyPlaces.value === true) {
      if (place.only_halal === false) {
        return false;
      }
    }
    // Apply rating filter
    if (place.distance > distanceFilter.value) {
      return false;
    }

    if (hideAlcoholPlaces.value === true) {
      if (place.serve_alcohal === true) {
        return false;
      }
    }

    if (ratingFilter.value) {
      if (place.rating < ratingFilter.value) return false;
    }

    // Filter by search query (case-insensitive)
    if (searchQuery.value) {
      const foundInDescription = place.decription
        .toLowerCase()
        .includes(searchQuery.value.toLowerCase());

      const foundInName = place.name
        .toLowerCase()
        .includes(searchQuery.value.toLowerCase());

      return foundInName || foundInDescription;
    }

    return true;
  });
});

const handleRatingUpdate = (value) => {
  ratingFilter.value = value;
};

const images = Array.from({ length: 10 }, (_, index) => ({
  id: index + 1,
  url: `https://picsum.photos/800/600?random=${index + 1}`,
}));

const carouselConfig = {
  height: 400,
  itemsToShow: 1.5,
  wrapAround: true,
};
</script>

<style scoped>
.header-text {
  font-size: 18px;
  font-weight: 400;
  line-height: 27px;
  color: white;
  text-align: center;
  margin-top: 8%;
}

.hadder {
  height: 600px;
  background-color: brown;
}

/* Store Buttons Styling */
.store-buttons {
  display: flex;
  justify-content: center;
  gap: 15px;
  margin-top: 20px;
}

.store-buttons img {
  height: 50px;
}

@media (max-width: 600px) {
  .store-badge {
    width: 140px;
    /* Smaller size on small screens */
  }
}

#kmRange::-webkit-slider-runnable-track {
  background: brown;
  height: 6px;
  border-radius: 5px;
}

#kmRange::-moz-range-track {
  background: brown;
  height: 6px;
  border-radius: 5px;
}

/* Style the thumb (slider handle) */
#kmRange::-webkit-slider-thumb {
  background: brown;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  cursor: pointer;
  margin-top: -5px;
  appearance: none;
}

#kmRange::-moz-range-thumb {
  background: brown;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  cursor: pointer;
}
</style>
