<template>
  <div>
    <v-container style="padding: 0px">
      <v-row class="contentFooter">
        <v-col
          cols="12"
          md="6"
          class="d-flex flex-column align-center align-md-start"
        >
          <div>
            <img alt="LogoVPN" :src="LogoVPN" width="148" height="40" />
          </div>
          <div>
            <span class="rubik-16-regular" style="color: #4f5665">
              <span class="rubik-16-medium" style="color: #4f5665"
                >LaslesVPN</span
              >
              is a private virtual network <br />
              that has unique features and has high security.
            </span>
          </div>
          <div class="d-flex justify-start align-center ga-3 mt-5">
            <button class="btn-icon">
              <span class="rubik-25-medium">f</span>
            </button>
            <button class="btn-icon">
              <v-icon size="20" color="orange-color">mdi-twitter</v-icon>
            </button>
            <button class="btn-icon">
              <v-icon size="20" color="orange-color">mdi-instagram</v-icon>
            </button>
          </div>
          <div class="mt-5">
            <span class="rubik-18-regular" style="color: #afb5c0"
              >©2020LaslesVPN</span
            >
          </div>
        </v-col>
        <v-col cols="12" md="6">
          <v-row>
            <v-col
              v-for="(section, idx) in footerSections"
              :key="idx"
              cols="4"
              class="d-flex flex-column align-center ga-3"
            >
              <span class="rubik-18-medium resetfont18" style="color: #0b132a">
                {{ section.title }}
              </span>
              <span
                v-for="(item, i) in section.items"
                :key="i"
                class="rubik-16-regular resetfont16"
                style="color: #4f5665"
              >
                {{ item }}
              </span>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script setup>
import LogoVPN from "@/assets/LogoVPN.svg";
import { ref } from "vue";

const footerSections = ref([
  {
    title: "Product",
    items: ["Download", "Pricing", "Locations", "Server", "Countries", "Blog"],
  },
  {
    title: "Engage",
    items: [
      "LaslesVPN ?",
      "FAQ",
      "Tutorials",
      "About Us",
      "Privacy Policy",
      "Terms of Service",
    ],
  },
  {
    title: "Earn Money",
    items: ["Affiliate", "Become Partner"],
  },
]);
</script>

<style scoped>
.contentFooter {
  margin: 0px 5px;
}
.btn-icon {
  background: #ffffff;
  border: 1px solid #ffffff;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 100%;
  width: 36px;
  height: 36px;
  margin-right: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #f53838;
}

@media only screen and (max-width: 452px) {
  .resetfont18 {
    font-size: 13px !important;
  }
  .resetfont16 {
    font-size: 10px !important;
  }
}
</style>
