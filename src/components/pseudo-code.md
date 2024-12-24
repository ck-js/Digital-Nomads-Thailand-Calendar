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
// implement mobile screen size solution 
// we want to conditionally render the day name element depending on the screen width i.e. only render to dom when screen width is larger than 768px



<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import dayjs from 'dayjs';
import EventItem from './EventItem.vue';

const props = defineProps({
  events: {
    type: Array,
    required: true,
  },
});

const today = ref(dayjs().date());
const currentMonth = ref(dayjs().format('MMMM'));
const currentYear = ref(dayjs().format('YYYY'));
const dayNameItems = ref(['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']);

// Reactive property to track screen width
const isWideScreen = ref(window.innerWidth > 768);

// Function to update isWideScreen based on window width
const updateScreenWidth = () => {
  isWideScreen.value = window.innerWidth > 768;
};

// Add event listener on mounted and remove on unmounted
onMounted(() => {
  window.addEventListener('resize', updateScreenWidth);
});

onUnmounted(() => {
  window.removeEventListener('resize', updateScreenWidth);
});

const preGridItems = computed(() => {
  const firstDayOfMonth = dayjs().date(1).day() + 2;
  return Array.from({ length: firstDayOfMonth }, (_, i) => ({}));
});

const gridItems = computed(() => {
  const daysInMonth = dayjs().daysInMonth();
  return Array.from({ length: daysInMonth }, (_, i) => {
    const date = dayjs().date(i + 1).format('YYYY-MM-DD');
    const dayEvents = props.events.filter(event => event.date === date);
    return {
      id: i + 1,
      date,
      events: dayEvents
    };
  });
});
console.log(gridItems.value);
</script>

<template>
  <h1>{{ today }} {{ currentMonth }}
    <span>{{ currentYear }}</span>
  </h1>

  <!-- Conditionally render day-name-container based on screen width -->
  <div v-if="isWideScreen" class="day-name-container">
    <div v-for="dayName in dayNameItems" :key="dayName">
      {{ dayName }}
    </div>
  </div>

  <div class="grid-container">
    <div v-for="item in preGridItems" class="grid-item">
      <span>{{ item.id }}</span>
    </div>
    <div v-for="item in gridItems" :key="item.id" class="grid-item" :class="{ today: item.id === today }">
      <span :style="Number(item.id) === Number(today) ? { backgroundColor: 'red', borderRadius: '50%' } : {}">
        {{ item.id }}
      </span>
      <EventItem 
        v-for="event in item.events"
        :key="event.title"
        :event="event"
      />
    </div>
  </div>
</template>

<style scoped>
.grid-container,
.day-name-container {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 1rem;
}

.grid-item {
  width: 100px;
  height: 100px;
}

.today {
  background-color: yellow; /* Highlight today's date */
}

.event-green {
  background-color: hsla(160, 100%, 37%, 1);
  color: black;
  height: 20%;
  margin-top: 5px; /* Add some space between events */
}

.event-green:hover {
  cursor: pointer;
}

@media (max-width: 768px) {
  .grid-container {
    display: flex;
    overflow-x: auto;
    scroll-snap-type: x mandatory; /* Enable scroll snap */
    scroll-behavior: smooth; /* Enable smooth scrolling */
    width: 100%;
    height: 100%;
    padding: 1rem; /* Add padding for better spacing */
  }

  .grid-item {
    flex: 0 0 150px;
    height: 100vh;
    scroll-snap-align: start; /* Align items to the start of the container */
    margin-right: 1rem; /* Add margin between items */
  }

  .grid-item:last-child {
    margin-right: 0; /* Remove margin for the last item */
  }
}
</style>