<template>
  <v-container>
    <v-row justify="space-around">
      <v-col cols="12">
        Selected Date (US Format): {{ formatUSDate() }}<br />
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
            >
              <!-- <template v-slot:actions>
                <v-row class="pa-2">
                  <v-col cols="12">
                    <v-btn
                      variant="outlined"
                      size="small"
                      @click="setDateRange('1day')"
                      class="mr-2 mb-2"
                    >
                      1 Day Ago
                    </v-btn>
                    <v-btn
                      variant="outlined"
                      size="small"
                      @click="setDateRange('1month')"
                      class="mr-2 mb-2"
                    >
                      1 Month Ago
                    </v-btn>
                    <v-btn
                      variant="outlined"
                      size="small"
                      @click="setDateRange('6months')"
                      class="mr-2 mb-2"
                    >
                      6 Months Ago
                    </v-btn>
                  </v-col>
                </v-row>
              </template> -->
              <template v-slot:actions>
                <v-row class="pa-2">
                  <v-col cols="12">
                    <v-btn
                      variant="outlined"
                      size="small"
                      @click="setDateRange('today')"
                      class="mr-2 mb-2"
                    >
                      Today
                    </v-btn>
                    <v-btn
                      variant="outlined"
                      size="small"
                      @click="setDateRange('1day')"
                      class="mr-2 mb-2"
                    >
                      1 Day Ago
                    </v-btn>
                    <v-btn
                      variant="outlined"
                      size="small"
                      @click="setDateRange('1week')"
                      class="mr-2 mb-2"
                    >
                      1 Week Ago
                    </v-btn>
                    <v-btn
                      variant="outlined"
                      size="small"
                      @click="setDateRange('1month')"
                      class="mr-2 mb-2"
                    >
                      1 Month Ago
                    </v-btn>
                    <v-btn
                      variant="outlined"
                      size="small"
                      @click="setDateRange('6months')"
                      class="mr-2 mb-2"
                    >
                      6 Months Ago
                    </v-btn>
                  </v-col>
                </v-row>
              </template>
            </v-date-picker>
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
      const lastDate = new Date(
        selectedDate.value[selectedDate.value.length - 1]
      );

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

/* const setDateRange = (period) => {
  const today = new Date();
  let startDate = new Date();

  switch (period) {
    case '1day':
      startDate.setDate(today.getDate() - 1);
      selectedDate.value = [startDate, today];
      break;
    case '1month':
      startDate.setMonth(today.getMonth() - 1);
      selectedDate.value = [startDate, today];
      break;
    case '6months':
      startDate.setMonth(today.getMonth() - 6);
      selectedDate.value = [startDate, today];
      break;
  }

  // Auto close the menu after selection
  menuOpen.value = false;
}; */
const setDateRange = (period) => {
  const today = new Date();
  let startDate = new Date();

  switch (period) {
    case "today":
      selectedDate.value = [today, today];
      break;
    case "1day":
      startDate.setDate(today.getDate() - 1);
      selectedDate.value = [startDate, today];
      break;
    case "1week":
      startDate.setDate(today.getDate() - 7);
      selectedDate.value = [startDate, today];
      break;
    case "1month":
      startDate.setMonth(today.getMonth() - 1);
      selectedDate.value = [startDate, today];
      break;
    case "6months":
      startDate.setMonth(today.getMonth() - 6);
      selectedDate.value = [startDate, today];
      break;
  }

  // Auto close the menu after selection
  menuOpen.value = false;
};
</script>
