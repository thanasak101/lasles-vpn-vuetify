<template>
  <div>
    <v-container>
      <v-row class="contentSubscribe text-center text-md-start">
        <v-col cols="12" md="6">
          <span class="rubik-35-medium" style="color: #0b132a">
            Subscribe Now for <br />
            Get Special Features!
          </span>
          <p class="rubik-16-regular" style="color: #4f5665">
            Let's subscribe with us and find the fun.
          </p>
        </v-col>
        <v-col cols="12" md="6" class="d-flex justify-center align-center">
          <v-btn
            size="large"
            color="orange-color"
            class="text-white px-8 py-3 btnSubscribe"
            rounded-xl
            width="250"
            height="60"
          >
            Subscribe Now
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script setup></script>

<style scoped>
.contentSubscribe {
  background: #ffffff;
  border: 2px solid #ffffff;
  border-radius: 10px;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  margin: 50px 5px 30px 5px;
  padding: 30px;
  display: flex;
  align-items: center;
}
.btnSubscribe {
  box-shadow: 0 12px 54px rgba(243, 78, 78, 0.54) !important;
  transition: all 0.3s ease !important;
}

.btnSubscribe:hover {
  box-shadow: 0 12px 25px rgba(243, 78, 78, 0.5) !important;
  transform: translateY(-2px);
}

.btnSubscribe:active {
  transform: translateY(0px);
  box-shadow: 0 6px 15px rgba(243, 78, 78, 0.3) !important;
}

@media only screen and (max-width: 425px) {
  .contentSubscribe {
    margin: 0px;
    padding: 0px;
  }
}
</style>
