<template>
  <v-container>
    <v-row justify="space-around">
      <v-col cols="12">
        Selected Date (ISO): {{ formatSelectedDateForDisplay() }}<br />
        Selected Date (US Format): {{ formatUSDate() }}<br />
        {{ formatSelectedDateForTemplate() }}<br />
        {{ formattedDate }}<br />
        {{ selectedDate }}<br />
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
              multiple="range"
            ></v-date-picker>
          </v-menu>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>
<script setup>
const selectedDate = ref([]);
/* const selectedDate = ref([
  new Date('2025-08-29'),
  new Date('2025-08-31')
]); */
const datePickerWrapper = ref(null);
const menuOpen = ref(false);

const openDatePicker = () => {
  menuOpen.value = true;
};

const clearDate = () => {
  selectedDate.value = [];
};

const onDateSelect = (date) => {
  selectedDate.value = date;
  if (Array.isArray(date) && date.length >= 2) {
    menuOpen.value = false;
  }
};

// Function to format selected dates for display
const formatSelectedDateForDisplay = () => {
  if (!selectedDate.value || selectedDate.value.length === 0) return "";

  if (Array.isArray(selectedDate.value)) {
    if (selectedDate.value.length === 1) {
      const date = selectedDate.value[0];
      return date instanceof Date
        ? date.toISOString()
        : new Date(date).toISOString();
    } else if (selectedDate.value.length >= 2) {
      // Show only first and last date
      const firstDate = selectedDate.value[0];
      const lastDate = selectedDate.value[selectedDate.value.length - 1];
      const firstISO =
        firstDate instanceof Date
          ? firstDate.toISOString()
          : new Date(firstDate).toISOString();
      const lastISO =
        lastDate instanceof Date
          ? lastDate.toISOString()
          : new Date(lastDate).toISOString();
      return `${firstISO} - ${lastISO}`;
    }
  }

  return selectedDate.value instanceof Date
    ? selectedDate.value.toISOString()
    : new Date(selectedDate.value).toISOString();
};

// Function to format selected dates for template display (Buddhist Era)
const formatSelectedDateForTemplate = () => {
  if (!selectedDate.value || selectedDate.value.length === 0) return "";

  if (Array.isArray(selectedDate.value) && selectedDate.value.length >= 2) {
    // For range selection, show only first and last date
    const firstDate = new Date(selectedDate.value[0]);
    const lastDate = new Date(
      selectedDate.value[selectedDate.value.length - 1]
    );

    const formatDate = (date) => {
      const day = date.getDate().toString().padStart(2, "0");
      const month = (date.getMonth() + 1).toString().padStart(2, "0");
      const buddhistYear = date.getFullYear() + 543;
      return `${day}/${month}/${buddhistYear}`;
    };

    return `${formatDate(firstDate)}-${formatDate(lastDate)}`;
  }

  if (Array.isArray(selectedDate.value) && selectedDate.value.length === 1) {
    const date = new Date(selectedDate.value[0]);
    const day = date.getDate().toString().padStart(2, "0");
    const month = (date.getMonth() + 1).toString().padStart(2, "0");
    const buddhistYear = date.getFullYear() + 543;
    return `${day}/${month}/${buddhistYear}`;
  }

  return "";
};

// Function to format dates in US format (MM/DD/YYYY)
const formatUSDate = () => {
  if (!selectedDate.value || selectedDate.value.length === 0) return "";

  if (Array.isArray(selectedDate.value)) {
    if (selectedDate.value.length === 1) {
      const date = new Date(selectedDate.value[0]);
      const year = date.getFullYear();
      const month = (date.getMonth() + 1).toString().padStart(2, "0");
      const day = date.getDate().toString().padStart(2, "0");
      return `[${year}-${month}-${day}]`;
    } else if (selectedDate.value.length >= 2) {
      // Show only first and last date
      const firstDate = new Date(selectedDate.value[0]);
      const lastDate = new Date(selectedDate.value[selectedDate.value.length - 1]);

      const formatDate = (date) => {
        const year = date.getFullYear();
        const month = (date.getMonth() + 1).toString().padStart(2, "0");
        const day = date.getDate().toString().padStart(2, "0");
        return `${year}-${month}-${day}`;
      };

      return `[${formatDate(firstDate)},${formatDate(lastDate)}]`;
    }
  }

  const date = new Date(selectedDate.value);
  const year = date.getFullYear();
  const month = (date.getMonth() + 1).toString().padStart(2, "0");
  const day = date.getDate().toString().padStart(2, "0");
  return `[${year}-${month}-${day}]`;
};

// Computed property to format date in Buddhist Era (DD/MM/YYYY+543)
const formattedDate = computed(() => {
  if (!selectedDate.value || selectedDate.value.length === 0) return "";

  if (Array.isArray(selectedDate.value)) {
    if (selectedDate.value.length === 1) {
      const date = new Date(selectedDate.value[0]);
      const day = date.getDate().toString().padStart(2, "0");
      const month = (date.getMonth() + 1).toString().padStart(2, "0");
      const buddhistYear = date.getFullYear() + 543;
      return `${day}/${month}/${buddhistYear}`;
    } else if (selectedDate.value.length >= 2) {
      // Show only first and last date for range
      const firstDate = new Date(selectedDate.value[0]);
      const lastDate = new Date(
        selectedDate.value[selectedDate.value.length - 1]
      );

      const formatDate = (date) => {
        const day = date.getDate().toString().padStart(2, "0");
        const month = (date.getMonth() + 1).toString().padStart(2, "0");
        const buddhistYear = date.getFullYear() + 543;
        return `${day}/${month}/${buddhistYear}`;
      };

      return `${formatDate(firstDate)}-${formatDate(lastDate)}`;
    }
  }

  const date = new Date(selectedDate.value);
  const day = date.getDate().toString().padStart(2, "0");
  const month = (date.getMonth() + 1).toString().padStart(2, "0");
  const buddhistYear = date.getFullYear() + 543;

  return `${day}/${month}/${buddhistYear}`;
});
</script>
