// define and store the current date, month and year as
reactive references
// create grid of 35 days or in other words 7 columns and 5 rows
// create days of the week container to render the day names similar to a table header
// insert dummy placeholder event and plan how it will be rendered onto the DOM


<script setup>
import { ref } from 'vue';
import Calendar from './components/Calendar.vue';

// Sample events data
const events = ref([
  { title: 'Event 1', date: '2023-10-01' },
  { title: 'Event 2', date: '2023-10-05' },
  { title: 'Event 3', date: '2023-10-10' },
]);
</script>

<template>
  <div id="app">
    <Calendar :events="events" />
  </div>
</template>

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

// Create an array to represent the grid items
const gridItems = computed(() => {
  const daysInMonth = dayjs().daysInMonth();
  return Array.from({ length: daysInMonth }, (_, i) => {
    const date = dayjs().date(i + 1).format('YYYY-MM-DD');
    const event = props.events.find(event => event.date === date);
    return {
      id: i + 1,
      date,
      title: event ? event.title : ''
    };
  });
});
</script>

<template>
  <h1>{{ today }} {{ currentMonth }}
    <span>{{ currentYear }}</span>
  </h1>

  <div class="grid-container">
    <div v-for="item in gridItems" :key="item.id" class="grid-item">
      <div>{{ item.date }}</div>
      <div>{{ item.title }}</div>
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
</style>