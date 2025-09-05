<template>
  <div>
    <v-container>
      <v-row>
        <v-col cols="12" class="d-flex flex-column ga-5 text-center">
          <h2 class="rubik-35-medium" style="color: #0b132a">
            Trusted by Thousands of <br />
            Happy Customer
          </h2>
          <span class="rubik-16-regular" style="color: #4f5665"
            >These are the stories of our customers who have joined us with
            great <br />
            pleasure when using our services.</span
          >
        </v-col>
        <v-col cols="12" class="text-center" style="margin-top: 80px">
          <swiper
            :slidesPerView="3"
            :centeredSlides="false"
            :pagination="pagination"
            :navigation="navigation"
            :modules="modules"
            :breakpoints="breakpoints"
            class="mySwiper"
            style="padding: 10px"
            :autoplay="{
              delay: 2500,
              disableOnInteraction: true,
            }"
          >
            <swiper-slide v-for="card in listcard" :key="card.id">
              <div class="card" style="padding: 25px 25px">
                <div
                  class="card-title d-flex justify-space-between align-center text-left ga-4 mb-3"
                >
                  <div class="d-flex align-center ga-5">
                    <img :src="card.image" :alt="card.name" />
                    <div>
                      <span class="rubik-18-medium" style="color: #0b132a">{{
                        card.name
                      }}</span>
                      <p class="rubik-14-regular" style="color: #4f5665">
                        {{ card.location }}
                      </p>
                    </div>
                  </div>
                  <div class="d-flex align-center ga-3">
                    <span>{{ card.rating }}</span>
                    <v-icon size="x-small" color="yellow-color"
                      >mdi-star</v-icon
                    >
                  </div>
                </div>
                <div class="card-content">
                  <p class="rubik-16-regular text-left" style="color: #0b132a">
                    {{ card.review }}
                  </p>
                </div>
              </div>
            </swiper-slide>
          </swiper>
          <!-- Custom navigation and pagination controls -->
          <div class="d-flex justify-space-between align-center mb-4">
            <div>
              <div class="swiper-pagination-custom"></div>
            </div>
            <div>
              <div class="swiper-button-prev-custom">
                <v-icon size="x-small">mdi-arrow-left</v-icon>
              </div>
              <div class="swiper-button-next-custom">
                <v-icon size="x-small">mdi-arrow-right</v-icon>
              </div>
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script setup>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";
// Import Swiper styles
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/navigation";
// import required modules
import { Pagination, Navigation, Autoplay } from "swiper/modules";
const modules = [Pagination, Navigation, Autoplay];

import customer1 from "@/assets/customer1.svg";
import customer2 from "@/assets/customer2.svg";
import customer3 from "@/assets/customer3.svg";

const breakpoints = {
  // when window width is >= 320px
  320: {
    slidesPerView: 1,
    spaceBetween: 10,
  },
  // when window width is >= 480px
  480: {
    slidesPerView: 1,
    spaceBetween: 10,
  },
  // when window width is >= 768px
  768: {
    slidesPerView: 2,
    spaceBetween: 10,
  },
  // when window width is >= 1440px
  1440: {
    slidesPerView: 3,
    spaceBetween: 20,
  },
};
// Use refs for custom elements
const navigation = {
  nextEl: ".swiper-button-next-custom",
  prevEl: ".swiper-button-prev-custom",
};
const pagination = {
  el: ".swiper-pagination-custom",
  clickable: true,
};

const listcard = [
  {
    id: 1,
    name: "Viezh Robert",
    location: "Warsaw, Poland",
    rating: 4.5,
    review:
      "“Wow... I am very happy to use this VPN, it turned out to be more than my expectations and so far there have been no problems. LaslesVPN always the best”.",
    image: customer1,
  },
  {
    id: 2,
    name: "Yessica Christy",
    location: "Shanxi, China",
    rating: 4.5,
    review:
      "“I like it because I like to travel far and still can connect with high speed.”.",
    image: customer2,
  },
  {
    id: 3,
    name: "Kim Young Jou",
    location: "Seoul, South Korea",
    rating: 4.5,
    review:
      "“This is very unusual for my business that currently requires a virtual private network that has high security.”.",
    image: customer3,
  },
  {
    id: 4,
    name: "Kim Young Jou",
    location: "Seoul, South Korea",
    rating: 4.5,
    review:
      "“This is very unusual for my business that currently requires a virtual private network that has high security.”.",
    image: customer3,
  },
  {
    id: 5,
    name: "Viezh Robert",
    location: "Warsaw, Poland",
    rating: 4.5,
    review:
      "“Wow... I am very happy to use this VPN, it turned out to be more than my expectations and so far there have been no problems. LaslesVPN always the best”.",
    image: customer1,
  },
  {
    id: 6,
    name: "Yessica Christy",
    location: "Shanxi, China",
    rating: 4.5,
    review:
      "“I like it because I like to travel far and still can connect with high speed.”.",
    image: customer2,
  },
];
</script>

<style scoped>
.swiper {
  width: 100%;
  height: 100%;
}

.swiper-slide {
  background: #ffffff;
  border: 2px solid #dddddd;
  border-radius: 10px;
}

.swiper {
  width: auto;
  height: auto;
  margin: 20px auto;
}

.swiper-button-prev-custom,
.swiper-button-next-custom {
  width: 35px;
  height: 35px;
  background: #fff;
  border-radius: 50%;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin: 0 8px;
  cursor: pointer;
  color: #f53838;
  font-size: 20px;
  border: 2px solid #f53838;
}

.swiper-button-prev-custom:hover,
.swiper-button-next-custom:hover {
  background: #f53838;
  color: #fff;
}

:deep(span.swiper-pagination-bullet) {
  width: 15px;
  height: 15px;
  background: #e53935;
}
:deep(span.swiper-pagination-bullet.swiper-pagination-bullet-active) {
  width: 45px !important;
  border-radius: 10px !important;
  background: #f53838 !important;
}

.card {
  min-height: 160px;
  height: 100%;
}
</style>
