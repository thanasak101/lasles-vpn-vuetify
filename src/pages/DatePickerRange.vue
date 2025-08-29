<template>
  <div class="d-flex justify-center">
    <v-date-input
      v-model="model"
      label="Select range"
      multiple="range"
      color="primary"
      class="custom-date-input"
    ></v-date-input>
  </div>
</template>

<script setup>
import { ref } from "vue";

const model = ref(null);
</script>

<style>
 button.v-btn.v-theme--myCustomLightTheme.v-btn--density-default.v-btn--rounded.v-btn--size-default.v-btn--variant-text{
  width: 75px !important;
 }
</style>
