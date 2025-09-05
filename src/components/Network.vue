<template>
  <div>
    <v-container class="mt-16">
      <v-row>
        <v-col cols="12" class=" d-flex flex-column ga-5 text-center">
          <h2 class="rubik-35-medium" style="color: #0b132a">
            Huge Global Network <br /> of Fast VPN
          </h2>
          <span class="rubik-16-regular" style="color: #4f5665">See <span class="rubik-16-medium">LaslesVPN</span> everywhere to make it easier for you when you move <br /> locations.</span>
        </v-col>
        <v-col cols="12" class="text-center" style="margin-top: 80px;">
          <img :src="network" alt="network" class="img">
        </v-col>
        <v-col cols="12" class="text-center">
          <img :src="sponsor" alt="network" class="img">
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script setup>
import network from '@/assets/network.svg';
import sponsor from '@/assets/sponsor.svg';
</script>

<style scoped>
.img {
  max-width: 100%;
  height: auto;
}
</style>
