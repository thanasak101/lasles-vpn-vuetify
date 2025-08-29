<template>
  <v-container>
    <v-row justify="space-around">
      <v-col cols="12">
        Selected Date (ISO): {{ selectedDate?.toISOString() }}
      </v-col>
      <v-col cols="12">
        <div ref="datePickerWrapper">
          <v-text-field
            :model-value="formattedDate"
            label="Date input (Buddhist Era)"
            readonly
            clearable
            append-inner-icon="mdi-calendar"
            @click:append-inner="openDatePicker"
            @click:clear="clearDate"
            @click="openDatePicker"
          ></v-text-field>

          <v-menu
            v-model="menuOpen"
            :close-on-content-click="false"
            location="bottom"
          >
            <template v-slot:activator="{ props }">
              <div v-bind="props" style="display: none"></div>
            </template>
            <v-date-picker
              color="primary"
              title="Select Date"
              v-model="selectedDate"
              @update:model-value="onDateSelect"
            ></v-date-picker>
          </v-menu>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>
<script setup>
const selectedDate = ref(new Date());
const datePickerWrapper = ref(null);
const menuOpen = ref(false);

const openDatePicker = () => {
  menuOpen.value = true;
};

const clearDate = () => {
  selectedDate.value = null;
};

const onDateSelect = (date) => {
  selectedDate.value = date;
  menuOpen.value = false;
};

// Computed property to format date in Buddhist Era (DD/MM/YYYY+543)
const formattedDate = computed(() => {
  if (!selectedDate.value) return "";

  const date = new Date(selectedDate.value);
  const day = date.getDate().toString().padStart(2, "0");
  const month = (date.getMonth() + 1).toString().padStart(2, "0");
  const buddhistYear = date.getFullYear() + 543;

  return `${day}/${month}/${buddhistYear}`;
});
</script>
<style scoped>
:deep(button.v-btn.v-btn--active.v-theme--myCustomLightTheme.bg-primary.v-btn--density-default.v-btn--rounded.v-btn--size-default.v-btn--variant-flat) {
  width: 95px !important;
}
</style>
