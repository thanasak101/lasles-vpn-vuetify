<template>
  <div>
    <v-container fluid class="pa-0 mt-10">
      <v-row no-gutters>
        <v-col
          cols="12"
          md="6"
          class="pa-8 pa-md-16 d-flex flex-column justify-center"
        >
          <div class="hero-content">
            <h1
              class="rubik-50-medium"
              style="color: #0b132a; line-height: 1.2"
            >
              Want anything to be <br />
              easy with LaslesVPN.
            </h1>

            <p
              class="text-body-1 text-grey-darken-1 mb-8"
              style="color: #4f5665; max-width: 600px"
            >
              Provide a network for all your needs with ease and fun using
              <span class="rubik-16-medium" style="color: #0b132a"
                >LaslesVPN</span
              >
              discover interesting features from us.
            </p>

            <v-btn
              size="large"
              color="orange-color"
              class="text-white px-8 py-3 btnStart"
              rounded-xl
              width="250"
              height="50"
            >
              Get Started
            </v-btn>
          </div>
        </v-col>

        <v-col cols="12" md="6" class="pa-8 d-flex flex-column justify-center">
          <div class="hero-image text-center">
            <!-- Hero illustration placeholder - you can replace with actual image -->
            <div class="illustration-container">
              <img :src="pic1" class="responsive-img" />
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
    <v-container>
      <v-row>
        <v-col cols="12" sm="4">
          <div class="d-flex justify-center ga-10">
            <img :src="stat1" />
            <div class="d-flex flex-column">
              <span class="rubik-25-bold" style="color: #0b132a">90+</span>
              <span class="rubik-20-regular" style="color: #4f5665;width: 91px;">Users</span>
            </div>
          </div>
        </v-col>
        <v-divider
          :thickness="1"
          class="border-opacity-25 vdivider"
          vertical
        ></v-divider>
        <v-col cols="12" sm="4">
          <div class="d-flex justify-center ga-10">
            <img :src="stat2" />
            <div class="d-flex flex-column">
              <span class="rubik-25-bold" style="color: #0b132a">30+</span>
              <span class="rubik-20-regular" style="color: #4f5665;width: 91px;"
                >Locations</span
              >
            </div>
          </div>
        </v-col>
        <v-divider
          :thickness="1"
          class="border-opacity-25 vdivider"
          vertical
        ></v-divider>
        <v-col cols="12" sm="4">
          <div class="d-flex justify-center ga-10">
            <img :src="stat3" />
            <div class="d-flex flex-column">
              <span class="rubik-25-bold" style="color: #0b132a">50+</span>
              <span class="rubik-20-regular" style="color: #4f5665;width: 91px;"
                >Servers</span
              >
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script setup>
import pic1 from "@/assets/Illustration1.svg";
import stat1 from "@/assets/stat1.svg";
import stat2 from "@/assets/stat2.svg";
import stat3 from "@/assets/stat3.svg";
</script>

<style scoped>
/* .min-height-screen {
  min-height: calc(100vh - 80px);
}
 */
.hero-illustration {
  width: 100%;
  max-width: 500px;
  height: auto;
}

.illustration-container {
  position: relative;
  animation: float 3s ease-in-out infinite;
}

.responsive-img {
  width: 100%;
  max-width: 600px;
  height: auto;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
}

.floating-elements {
  animation: float 4s ease-in-out infinite reverse;
}

/* Responsive adjustments */
@media (max-width: 599.78px) {
  .vdivider{
    display: none;
  }
}
@media (max-width: 960px) {
  .hero-content {
    display: flex;
    flex-flow: column;
    justify-content: center;
    align-items: center;
    text-align: center;
  }
}

.btnStart {
  box-shadow: 0 8px 20px rgba(243, 78, 78, 0.4) !important;
  transition: all 0.3s ease !important;
}

.btnStart:hover {
  box-shadow: 0 12px 25px rgba(243, 78, 78, 0.5) !important;
  transform: translateY(-2px);
}

.btnStart:active {
  transform: translateY(0px);
  box-shadow: 0 6px 15px rgba(243, 78, 78, 0.3) !important;
}

.divStat {
  border-right: 1px solid #eeeff2;
}
</style>
