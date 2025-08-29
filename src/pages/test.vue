<template>
  <v-container>
    <v-row justify="space-around">
      <v-col cols="12">
        Selected Date (ISO): {{ selectedDate?.toISOString() }}
      </v-col>
      <v-col cols="12">
        <div ref="datePickerWrapper">
          <v-text-field
            :model-value="buddhistDisplayValue"
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
              <div v-bind="props" style="display: none;"></div>
            </template>
            <v-date-picker
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
import { ref, computed, nextTick, onBeforeUnmount, watch } from 'vue'
import { format } from 'date-fns'
import { th } from 'date-fns/locale'

const selectedDate = ref(new Date())
const datePickerWrapper = ref(null)
const menuOpen = ref(false)
let observer = null

// Thai month names
const thaiMonths = [
  'มกราคม', 'กุมภาพันธ์', 'มีนาคม', 'เมษายน', 'พฤษภาคม', 'มิถุนายน',
  'กรกฎาคม', 'สิงหาคม', 'กันยายน', 'ตุลาคม', 'พฤศจิกายน', 'ธันวาคม'
]

// Short Thai month names
const thaiMonthsShort = [
  'ม.ค.', 'ก.พ.', 'มี.ค.', 'เม.ย.', 'พ.ค.', 'มิ.ย.',
  'ก.ค.', 'ส.ค.', 'ก.ย.', 'ต.ค.', 'พ.ย.', 'ธ.ค.'
]

// Computed property for Buddhist Era display
const buddhistDisplayValue = computed(() => {
  if (!selectedDate.value) return ''

  const buddhistDate = new Date(selectedDate.value)
  buddhistDate.setFullYear(buddhistDate.getFullYear() + 543)

  return format(buddhistDate, 'dd/MM/yyyy', { locale: th })
})

const openDatePicker = () => {
  menuOpen.value = true
}

const clearDate = () => {
  selectedDate.value = null
}

const onDateSelect = (date) => {
  selectedDate.value = date
  menuOpen.value = false
}

const convertYearInPicker = () => {
  // Convert year in all possible locations
  const yearSelectors = [
    '.v-date-picker-header__value button',
    '.v-date-picker-title',
    '.v-picker-title',
    '.v-date-picker-header .v-btn',
    '.v-date-picker-controls .v-btn'
  ];

  // Also search in overlay
  const containers = [datePickerWrapper.value, document.querySelector('.v-overlay.v-menu')];

  containers.forEach(container => {
    if (!container) return;

    yearSelectors.forEach(selector => {
      const elements = container.querySelectorAll(selector);
      elements.forEach(element => {
        if (element && element.textContent) {
          let text = element.textContent;
          const yearMatch = text.match(/\b(\d{4})\b/g);
          if (yearMatch) {
            yearMatch.forEach(year => {
              const gregorianYear = parseInt(year, 10);
              if (gregorianYear >= 1900 && gregorianYear < 2500) {
                text = text.replace(year, gregorianYear + 543);
              }
            });
            element.textContent = text;
          }
        }
      });
    });

    // Convert years in the year selection list
    const yearButtons = container.querySelectorAll('.v-date-picker-years .v-btn');
    yearButtons.forEach(btn => {
      const contentElement = btn.querySelector('.v-btn__content');
      if (contentElement) {
        const gregorianYear = parseInt(contentElement.textContent, 10);
        if (!isNaN(gregorianYear) && gregorianYear >= 1900 && gregorianYear < 2500) {
          contentElement.textContent = gregorianYear + 543;
        }
      }
    });
  });
};

const convertMonthsInPicker = () => {
  const containers = [datePickerWrapper.value, document.querySelector('.v-overlay.v-menu')];

  containers.forEach(container => {
    if (!container) return;

    // Convert month buttons in month selection view
    const monthSelectors = [
      '.v-date-picker-months .v-btn',
      '.v-date-picker-month .v-btn',
      '.v-picker-month .v-btn',
      '[class*="month"] .v-btn'
    ];

    monthSelectors.forEach(selector => {
      const monthButtons = container.querySelectorAll(selector);
      if (monthButtons.length === 12) { // Ensure we have 12 month buttons
        monthButtons.forEach((btn, index) => {
          if (index < thaiMonthsShort.length) {
            const contentElement = btn.querySelector('.v-btn__content') || btn;
            if (contentElement) {
              contentElement.textContent = thaiMonthsShort[index];
            }
          }
        });
      }
    });

    // Convert month names in headers and titles
    const headerSelectors = [
      '.v-date-picker-header__value',
      '.v-date-picker-header__content',
      '.v-date-picker-title',
      '.v-picker-title',
      '.v-date-picker-controls .v-btn'
    ];

    headerSelectors.forEach(selector => {
      const elements = container.querySelectorAll(selector);
      elements.forEach(element => {
        if (element && element.textContent) {
          let text = element.textContent;

          // Convert full English month names to Thai
          const englishMonths = [
            'January', 'February', 'March', 'April', 'May', 'June',
            'July', 'August', 'September', 'October', 'November', 'December'
          ];

          // Convert short English month names to Thai
          const englishMonthsShort = [
            'Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
            'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'
          ];

          englishMonths.forEach((englishMonth, index) => {
            if (text.includes(englishMonth)) {
              text = text.replace(englishMonth, thaiMonths[index]);
            }
          });

          englishMonthsShort.forEach((englishMonth, index) => {
            if (text.includes(englishMonth)) {
              text = text.replace(englishMonth, thaiMonthsShort[index]);
            }
          });

          // Convert day names to Thai
          const englishDays = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
          const thaiDays = ['อา.', 'จ.', 'อ.', 'พ.', 'พฤ.', 'ศ.', 'ส.'];

          englishDays.forEach((englishDay, index) => {
            if (text.includes(englishDay)) {
              text = text.replace(englishDay, thaiDays[index]);
            }
          });

          if (text !== element.textContent) {
            element.textContent = text;
          }
        }
      });
    });
  });
};

const convertDayHeadersInPicker = () => {
  const containers = [datePickerWrapper.value, document.querySelector('.v-overlay.v-menu')];

  containers.forEach(container => {
    if (!container) return;

    // More specific selectors for Vuetify date picker day headers
    const dayHeaderSelectors = [
      '.v-date-picker-month__days thead th',
      '.v-date-picker-month__day-header',
      '.v-date-picker-table thead th',
      '.v-date-picker__table thead th',
      '.v-picker__body thead th',
      'table thead th',
      'thead th'
    ];

    let converted = false;

    dayHeaderSelectors.forEach(selector => {
      if (converted) return; // Skip if already converted

      const dayHeaders = container.querySelectorAll(selector);

      if (dayHeaders.length === 7) { // Should be 7 days
        const thaiDayHeaders = ['อา', 'จ', 'อ', 'พ', 'พฤ', 'ศ', 'ส'];

        dayHeaders.forEach((header, index) => {
          if (index < thaiDayHeaders.length) {
            const textContent = header.textContent.trim();
            const englishDays = ['S', 'M', 'T', 'W', 'T', 'F', 'S'];
            const fullEnglishDays = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];

            // Check if it's an English day header
            if (englishDays.includes(textContent) || fullEnglishDays.includes(textContent)) {
              header.textContent = thaiDayHeaders[index];
              converted = true;
            }
          }
        });
      }
    });

    // Alternative approach: find all elements with day letters and convert them
    if (!converted) {
      const allElements = container.querySelectorAll('*');
      const dayLetters = ['S', 'M', 'T', 'W', 'F']; // Note: T appears twice
      const thaiDayHeaders = ['อา', 'จ', 'อ', 'พ', 'พฤ', 'ศ', 'ส'];

      let foundHeaders = [];

      allElements.forEach(element => {
        const text = element.textContent.trim();
        if (text.length === 1 && dayLetters.includes(text)) {
          // Check if this element is likely a day header (not a date number)
          const parent = element.closest('thead, .v-date-picker-month__days');
          if (parent || element.tagName === 'TH') {
            foundHeaders.push(element);
          }
        }
      });

      // If we found exactly 7 headers, convert them
      if (foundHeaders.length === 7) {
        foundHeaders.forEach((header, index) => {
          header.textContent = thaiDayHeaders[index];
        });
      }
    }

    // Also check for abbr tags or spans within headers
    const dayAbbrs = container.querySelectorAll('thead th abbr, thead th span, th abbr, th span');
    if (dayAbbrs.length === 7) {
      const thaiDayHeaders = ['อา', 'จ', 'อ', 'พ', 'พฤ', 'ศ', 'ส'];

      dayAbbrs.forEach((abbr, index) => {
        if (index < thaiDayHeaders.length) {
          const text = abbr.textContent.trim();
          if (['S', 'M', 'T', 'W', 'F'].includes(text) || text.length <= 3) {
            abbr.textContent = thaiDayHeaders[index];
          }
        }
      });
    }
  });
};

const convertPickerContent = () => {
  convertYearInPicker();
  convertMonthsInPicker();
  convertDayHeadersInPicker();
};

// Watch for menu open/close
watch(menuOpen, (isOpen) => {
  if (isOpen) {
    nextTick(() => {
      // Multiple attempts with different delays
      setTimeout(() => convertPickerContent(), 50);
      setTimeout(() => convertPickerContent(), 150);
      setTimeout(() => convertPickerContent(), 300);

      const pickerContent = document.querySelector('.v-overlay.v-menu .v-date-picker') ||
                           document.querySelector('.v-overlay.v-menu [class*="picker"]');

      if (pickerContent && !observer) {
        observer = new MutationObserver((mutations) => {
          let shouldConvert = false;
          mutations.forEach(mutation => {
            if (mutation.type === 'childList' || mutation.type === 'attributes') {
              shouldConvert = true;
            }
          });

          if (shouldConvert) {
            setTimeout(() => convertPickerContent(), 10);
          }
        });

        observer.observe(pickerContent, {
          childList: true,
          subtree: true,
          attributes: true,
          attributeFilter: ['class'],
          characterData: true
        });
      }
    });
  } else if (observer) {
    observer.disconnect();
    observer = null;
  }
});

onBeforeUnmount(() => {
  if (observer) {
    observer.disconnect();
  }
});
</script>
