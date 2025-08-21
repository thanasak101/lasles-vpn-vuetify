<template>
  <!-- Navigation Drawer for Mobile -->
  <v-navigation-drawer
    v-model="drawer"
    app
    temporary
    location="left"
    width="280"
    class="d-lg-none"
  >
    <v-list>
      <v-list-item class="px-4 py-4">
        <div class="d-flex align-center">
          <img alt="LogoVPN" :src="LogoVPN" width="148" height="40" class="mr-3" />
        </div>
      </v-list-item>

      <v-divider></v-divider>

      <v-list-item
        v-for="item in menu"
        :key="item"
        class="px-4"
        @click="closeDrawer"
      >
        <v-list-item-title class="rubik-16 listMenu">{{ item }}</v-list-item-title>
      </v-list-item>

      <v-divider class="my-4"></v-divider>

      <div class="px-4 pb-4 d-flex flex-column">
        <v-btn
          color="blue-color"
          class="rubik-16-medium"
          variant="text"
        >
          Sign In
        </v-btn>
        <v-btn
          color="red-color"
          variant="outlined"
          block
          rounded
        >
          Sign Up
        </v-btn>
      </div>
    </v-list>
  </v-navigation-drawer>

  <!-- App Bar -->
  <v-app-bar color="white" :elevation="0" height="80" app style="border: none;">
    <v-container fluid class="px-4 px-md-8">
      <div class="d-flex align-center justify-start justify-md-space-between w-100">
        <!-- Mobile Menu Button -->
        <v-app-bar-nav-icon
          class="d-lg-none"
          @click="drawer = !drawer"
        ></v-app-bar-nav-icon>

        <!-- Logo -->
        <div class="d-flex align-center">
          <img alt="LogoVPN" :src="LogoVPN" width="148" height="40" class="ml-10" />
        </div>

        <!-- Desktop Menu -->
        <div class="d-none d-lg-flex align-center">
          <v-btn
            v-for="item in menu"
            :key="item"
            class="mx-1"
            color="secondary-color"
          >
            <span class="rubik-16">{{ item }}</span>
          </v-btn>
        </div>

        <!-- Desktop Auth Buttons -->
        <div class="d-none d-lg-flex align-center ga-4">
          <v-btn
            color="blue-color"
            class="rubik-16-medium"
          >
            Sign In
          </v-btn>
          <v-btn
            variant="outlined"
            color="red-color"
            class="rubik-16-medium px-6"
            rounded
          >
            Sign Up
          </v-btn>
        </div>

        <!-- Mobile Logo (when drawer button is present) -->
        <div class="d-lg-none"></div>
      </div>
    </v-container>
  </v-app-bar>
</template>

<script setup>
import { ref } from "vue";
import LogoVPN from "@/assets/LogoVPN.svg";

const menu = ref(["About", "Features", "Pricing", "Testimonials", "Help"]);
const drawer = ref(false);

const closeDrawer = () => {
  drawer.value = false;
};
</script>

<style scoped>
/* Remove custom button styles and use Vuetify defaults with some customization */
.v-btn {
  text-transform: none !important;
  font-weight: 500;
}

/* Custom styles for the navigation drawer */
.v-navigation-drawer .v-list-item {
  border-radius: 8px;
  margin: 4px 8px;
}

.v-navigation-drawer .v-list-item:hover {
  background-color: rgba(245, 56, 85, 0.1);
}

/* Ensure proper spacing and alignment */
.v-app-bar {
  border-bottom: 1px solid rgba(0, 0, 0, 0.05);
}

/* Mobile responsiveness */
@media (max-width: 1023px) {
  .v-app-bar-title {
    font-size: 1.1rem !important;
  }
}

@media (max-width: 599px) {
  .v-app-bar-title {
    font-size: 1rem !important;
  }
}

.listMenu{
  color: #4F5665;
}
</style>
