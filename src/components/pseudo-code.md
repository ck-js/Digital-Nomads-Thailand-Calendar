// define and store the current date, month and year as
reactive references
// create grid of 35 days or in other words 7 columns and 5 rows
// create days of the week container to render the day names similar to a table header
// insert dummy placeholder event and plan how it will be rendered onto the DOM
// use v-if attribute to conditionally render events by whether the title property of the reactive gridItems array of objects is true or false
// make the first date of the month start on the correct day
// it just so happens that 01/12 begins on day 0 which is Sunday, so we need to try lets say when 01/12 begins on a Teusday or day 2
// ok its an interesting problem that we eventually need to solve and we're lucky that 01/12 falls on Sunday
// the proposed solution is to add empty objects to our gridItems array.
// also think we should seperate the concerns between the fixed calendar items such as start day of the month and the date span item
// conditionally render the today class to indicate round red background 
// now events render dynamically with the events property of the gridItems array that is an array of objects 
// however it does not add more than 1 event to the same date
// try to implement a solution



<script setup>
import { ref, computed } from 'vue';
import dayjs from 'dayjs';

// Define props
const props = defineProps({
  events: {
    type: Array,
    required: true
  }
});

const today = ref(dayjs().format('DD'));
const currentMonth = ref(dayjs().format('MMMM'));
const currentYear = ref(dayjs().format('YYYY'));

// Calculate the first day of the month and its day of the week
const firstDayOfMonth = dayjs().startOf('month');
const firstDayOfWeek = firstDayOfMonth.day(); // 0 (Sunday) to 6 (Saturday)

// Create an array to represent the grid items
const gridItems = computed(() => {
  const daysInMonth = dayjs().daysInMonth();
  const items = [];

  // Add empty items for the days before the first day of the month
  for (let i = 0; i < firstDayOfWeek; i++) {
    items.push({ id: null, date: null, title: '' });
  }

  // Add items for each day of the month
  for (let i = 0; i < daysInMonth; i++) {
    const date = firstDayOfMonth.date(i + 1).format('YYYY-MM-DD');
    const event = props.events.find(event => event.date === date);
    items.push({
      id: i + 1,
      date,
      title: event ? event.title : ''
    });
  }

  return items;
});
</script>

<template>
  <h1>{{ today }} {{ currentMonth }}
    <span>{{ currentYear }}</span>
  </h1>

  <div class="day-name-container">
    <div v-for="dayName in dayNameItems" :key="dayName">
      {{ dayName }}
    </div>
  </div>

  <div class="grid-container">
    <div v-for="item in gridItems" :key="item.id || 'empty'" class="grid-item">
      <span v-if="item.id">{{ item.id }}</span>
      <div v-if="item.title" class="event-green">{{ item.title }}</div>
    </div>
  </div>
</template>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: repeat(7, 1fr); /* 7 columns for a week */
  gap: 10px;
}

.grid-item {
  background-color: #f0f0f0;
  padding: 10px;
  text-align: center;
}

.event-green {
  background-color: green;
  color: white;
  padding: 5px;
  border-radius: 3px;
}
</style>






<script setup>
import { ref, computed } from 'vue';
import dayjs from 'dayjs';

// Define props
const props = defineProps({
  events: {
    type: Array,
    required: true
  }
});

const today = ref(dayjs().date());
const currentMonth = ref(dayjs().format('MMMM'));
const currentYear = ref(dayjs().format('YYYY'));

// Calculate the first day of the month and its day of the week
const firstDayOfMonth = dayjs().startOf('month');
const firstDayOfWeek = firstDayOfMonth.day(); // 0 (Sunday) to 6 (Saturday)

// Create an array to represent the grid items
const gridItems = computed(() => {
  const daysInMonth = dayjs().daysInMonth();
  const items = [];

  // Add empty items for the days before the first day of the month
  for (let i = 0; i < firstDayOfWeek; i++) {
    items.push({ id: null, date: null, title: '' });
  }

  // Add items for each day of the month
  for (let i = 0; i < daysInMonth; i++) {
    const date = firstDayOfMonth.date(i + 1).format('YYYY-MM-DD');
    const event = props.events.find(event => event.date === date);
    items.push({
      id: i + 1,
      date,
      title: event ? event.title : ''
    });
  }

  return items;
});
</script>

<template>
  <h1>{{ today }} {{ currentMonth }}
    <span>{{ currentYear }}</span>
  </h1>

  <div class="day-name-container">
    <div v-for="dayName in dayNameItems" :key="dayName">
      {{ dayName }}
    </div>
  </div>

  <div class="grid-container">
    <div v-for="item in gridItems" :key="item.id || 'empty'" class="grid-item" :class="{ today: item.id === today }">
      <span :style="item.id === 15 ? { color: 'red', fontWeight: 'bold' } : {}">{{ item.id }}</span>
      <div v-if="item.title" class="event-green">{{ item.title }}</div>
    </div>
  </div>
</template>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: repeat(7, 1fr); /* 7 columns for a week */
  gap: 10px;
}

.grid-item {
  background-color: #f0f0f0;
  padding: 10px;
  text-align: center;
}

.today {
  background-color: yellow; /* Highlight today's date */
}

.event-green {
  background-color: green;
  color: white;
  padding: 5px;
  border-radius: 3px;
}
</style>