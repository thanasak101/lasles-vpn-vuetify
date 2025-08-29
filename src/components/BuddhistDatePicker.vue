<template>
  <div class="buddhist-datepicker">
    <!-- Custom Header with Buddhist Year -->
    <div class="datepicker-header mb-3 pa-3 bg-primary-lighten-5 rounded">
      <div class="d-flex justify-space-between align-center">
        <v-btn 
          icon 
          size="small" 
          @click="previousMonth"
          class="me-2"
        >
          <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
        
        <div class="text-center flex-grow-1">
          <div class="text-h6 font-weight-medium">
            {{ currentMonthName }} {{ buddhistYear }}
          </div>
          <div class="text-caption text-grey-darken-1">
            พ.ศ. {{ buddhistYear }} ({{ gregorianYear }})
          </div>
        </div>
        
        <v-btn 
          icon 
          size="small" 
          @click="nextMonth"
          class="ms-2"
        >
          <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </div>
    </div>
    
    <!-- Regular Datepicker (you can hide its header if possible) -->
    <Datepicker 
      v-model="internalDate" 
      :format="formatDisplayDate"
      @update:modelValue="onDateChange"
    />
    
    <!-- Buddhist Date Display -->
    <div class="mt-3 pa-3 bg-success-lighten-5 rounded">
      <div class="text-subtitle-2 mb-1">วันที่ที่เลือก (Buddhist Calendar):</div>
      <div class="text-body-1 font-weight-medium">
        {{ formatBuddhistDate(internalDate) }}
      </div>
      <div class="text-caption text-grey-darken-1">
        Gregorian: {{ formatGregorianDate(internalDate) }}
      </div>
    </div>
  </div>
</template>

<script setup>
import Datepicker from 'vue3-datepicker'
import { ref, computed, watch } from 'vue'
import { 
  format, 
  getYear, 
  getMonth, 
  addMonths, 
  subMonths,
  setMonth,
  setYear 
} from 'date-fns'
import { th } from 'date-fns/locale'

// Props
const props = defineProps({
  modelValue: {
    type: Date,
    default: () => new Date()
  }
})

// Emits
const emit = defineEmits(['update:modelValue'])

// Internal date state
const internalDate = ref(props.modelValue || new Date())

// Watch for external changes
watch(() => props.modelValue, (newValue) => {
  if (newValue) {
    internalDate.value = newValue
  }
})

// Buddhist year calculation (Gregorian + 543)
const buddhistYear = computed(() => {
  return getYear(internalDate.value) + 543
})

const gregorianYear = computed(() => {
  return getYear(internalDate.value)
})

const currentMonthName = computed(() => {
  return format(internalDate.value, 'MMMM', { locale: th })
})

// Date formatting functions
const formatBuddhistYear = (date) => {
  return getYear(date) + 543
}

const formatBuddhistDate = (date) => {
  const day = format(date, 'dd')
  const month = format(date, 'MMMM', { locale: th })
  const buddhYear = formatBuddhistYear(date)
  return `${day} ${month} พ.ศ. ${buddhYear}`
}

const formatGregorianDate = (date) => {
  return format(date, 'dd MMMM yyyy')
}

const formatDisplayDate = (date) => {
  const buddhYear = formatBuddhistYear(date)
  return format(date, 'dd/MM/') + buddhYear
}

// Navigation functions
const previousMonth = () => {
  internalDate.value = subMonths(internalDate.value, 1)
  emit('update:modelValue', internalDate.value)
}

const nextMonth = () => {
  internalDate.value = addMonths(internalDate.value, 1)
  emit('update:modelValue', internalDate.value)
}

// Handle date change from datepicker
const onDateChange = (newDate) => {
  internalDate.value = newDate
  emit('update:modelValue', newDate)
}
</script>

<style scoped>
.buddhist-datepicker {
  max-width: 400px;
}

.datepicker-header {
  border: 1px solid rgba(var(--v-theme-primary), 0.2);
}

/* Hide the default datepicker header if possible */
:deep(.vue3-datepicker__header) {
  display: none;
}

/* Custom styling for better visual appeal */
.v-btn {
  min-width: 40px !important;
}
</style>
