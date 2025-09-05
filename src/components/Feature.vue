<template>
  <div>
    <v-container class="d-flex justify-center align-center text-center mt-12">
      <v-row>
        <v-col cols="12" md="7">
          <img :src="feature" class="imgFeature" alt="feature" />
        </v-col>
        <v-col cols="12" md="5" class="d-flex flex-column justify-center align-center align-md-start">
          <v-row class="d-flex align-center">
            <v-col cols="12" class="pa-0">
              <div class="text-left">
                <span class="rubik-35-medium" style="color: #0b132a"
                  >We Provide Many <br />
                  Features You Can Use</span
                >
                <p class="rubik-16-regular mt-3" style="color: #4f5665">
                  You can explore the features that we provide with fun <br />
                  and have their own functions each feature.
                </p>
              </div>
              <div class="d-flex flex-column ga-2 mt-7">
                <div class="d-flex align-center" v-for="(item, index) in contentFeature" :key="index">
                  <img :src="item.icon" alt="checkboxMarkedMircle" />
                  <span
                    class="rubik-14-regular"
                    style="color: #4f5665; margin-left: 8px"
                    >{{ item.title }}</span
                  >
                </div>
              </div>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script setup>
import feature from "@/assets/feature.svg";
import checkboxMarkedMircle from "@/assets/checkbox-marked-circle.svg";

import { ref } from "vue";

const contentFeature = ref([
  {
    title: "Powerfull online protection.",
    icon: checkboxMarkedMircle,
  },
  {
    title: "Internet without borders.",
    icon: checkboxMarkedMircle,
  },
  {
    title: "Supercharged VPN",
    icon: checkboxMarkedMircle,
  },
  {
    title: "No specific time limits.",
    icon: checkboxMarkedMircle,
  }
]);
</script>

<style scoped>
.imgFeature {
  width: 100%;
  max-width: 509px;
  height: auto;
}
</style>
