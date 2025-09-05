<template>
  <div>
    <v-container>
      <v-row class="mt-10">
        <v-col cols="12" class="text-center">
          <h2 class="rubik-35-medium" style="color: #0b132a">
            Choose Your Plan
          </h2>
          <p class="rubik-16-regular" style="color: #4f5665">
            Let's choose the package that is best for you and explore it happily
            and <br />
            cheerfully.
          </p>
        </v-col>
      </v-row>
      <v-row>
        <v-col
          cols="12"
          md
          ="4"
          v-for="(plan, index) in selectPlan"
          :key="index"
          class="mt-7"
        >
          <v-card
            class="cardPlan d-flex flex-column align-center"
            elevation="1"
          >
            <v-container>
              <v-row class="d-flex justify-center mt-8">
                <v-col cols="12" md="4" class="d-flex justify-center">
                  <div class="d-flex flex-column text-center">
                    <img :src="plan.icon" alt="plan" class="mb-5" />
                    <span class="rubik-18-medium pt-5">{{ plan.text }}</span>
                  </div>
                </v-col>
              </v-row>
              <v-row class="d-flex justify-center mt-5">
                <div class="d-flex flex-column ga-4">
                  <div
                    class="d-flex align-center"
                    v-for="(feature, index) in plan.features"
                    :key="index"
                  >
                    <img :src="feature.icon" alt="checkboxMarkedMircle" />
                    <span
                      class="rubik-14-regular"
                      style="color: #4f5665; margin-left: 15px"
                      >{{ feature.text }}</span
                    >
                  </div>
                </div>
              </v-row>
            </v-container>
            <div class="d-flex flex-column align-center ga-3 mt-auto mb-8">
              <span class="d-flex align-center"
                ><p class="rubik-25-medium" style="color: #0B132A">{{ plan.price.number }}</p>
                <p class="rubik-25-regular" style="color: #4f5665; margin-left: 5px">{{ plan.price.unit }}</p></span
              >
              <v-btn class="btnSelect rubik-16-bold" elevation="0"> Select </v-btn>
            </div>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script setup>
import plan from "@/assets/plan.svg";
import check from "@/assets/check.svg";
import { ref } from "vue";

const selectPlan = ref([
  {
    icon: plan,
    text: "Free Plan",
    features: [
      { text: "Unlimited Bandwitch", icon: check },
      { text: "Encrypted Connection", icon: check },
      { text: "No Traffic Logs", icon: check },
      { text: "Works on All Devices", icon: check },
    ],
    price: {
      number: "Free",
      unit: "",
    },
  },
  {
    icon: plan,
    text: "Standard Plan",
    features: [
      { text: "Unlimited Bandwitch", icon: check },
      { text: "Encrypted Connection", icon: check },
      { text: "Yes Traffic Logs", icon: check },
      { text: "Works on All Devices", icon: check },
      { text: "Connect Anyware", icon: check },
    ],
    price: {
      number: "$9",
      unit: "/ mo",
    },
  },
  {
    icon: plan,
    text: "Premium Plan",
    features: [
      { text: "Unlimited Bandwitch", icon: check },
      { text: "Encrypted Connection", icon: check },
      { text: "Yes Traffic Logs", icon: check },
      { text: "Works on All Devices", icon: check },
      { text: "Connect Anyware", icon: check },
      { text: "Get New Features", icon: check },
    ],
    price: {
      number: "$12",
      unit: "/ mo",
    },
  },
]);
</script>

<style scoped>
.cardPlan {
  min-height: 760px;
  height: 100%;
  border-radius: 10px;
  border: 1px solid #dddddd;
  box-shadow: 5px 15px 5px #dddddd;
}
.btnSelect {
  background-color: #ffffff;
  color: #F53838;
  text-transform: none;
  width: 178px;
  height: 45px;
  border-radius: 50px;
  border: 2px solid #F53838;
}
.btnSelect:hover {
  background-color: #F53838;
  color: #ffffff;
  box-shadow: 0 10px 25px rgba(243, 78, 78, 0.5) !important
}
</style>
