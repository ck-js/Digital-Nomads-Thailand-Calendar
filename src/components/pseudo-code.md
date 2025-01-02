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
// in mobile version we want to place todays grid item block as the start grid container item so that users can start scroll from current date
// utilized the scroll into view method and make sure to assign id attribute to the relevcant item dynamically using v-bind directive 
// now implement pop up modal when an event is clicked to reveal more details
// set key down event handler to Esc and enter key to emit the close event which closes the modal or sets the show ref to false
// fix mobile event modal styling 
// refactor events data structure to utilize modules of classes with constructors for variant properties such as date and link
// '' brainstorm and plan pagination for toggling between months
// pagination controls now render previous and next months and year according to today ref
// we now need the grid to reflect the previous and next months and rerender the DOM
// make previous month to reflect in the Calendar grid item



<script setup>
// filepath: /Users/ck/Desktop/Code/DNT Calendar/vue-project/src/components/Calendar.vue
import { ref } from 'vue';
import dayjs from 'dayjs';
import EventItem from './EventItem.vue';

const currentMonth = ref(dayjs());
const today = dayjs().date();

const previousMonth = () => {
  currentMonth.value = currentMonth.value.subtract(1, 'month');
};

const nextMonth = () => {
  currentMonth.value = currentMonth.value.add(1, 'month');
};

const daysInMonth = (month) => {
  const startOfMonth = month.startOf('month');
  const endOfMonth = month.endOf('month');
  const days = [];
  for (let day = startOfMonth; day.isBefore(endOfMonth) || day.isSame(endOfMonth); day = day.add(1, 'day')) {
    days.push({
      id: day.date(),
      events: [] // Add logic to populate events for each day
    });
  }
  return days;
};

const days = ref(daysInMonth(currentMonth.value));

watch(currentMonth, (newMonth) => {
  days.value = daysInMonth(newMonth);
});
</script>

<template>
  <div>
    <button @click="previousMonth">Previous Month</button>
    <button @click="nextMonth">Next Month</button>
    <h2>{{ currentMonth.format('MMMM YYYY') }}</h2>
    <div class="calendar-grid">
      <div
        v-for="item in days"
        :key="item.id"
        :id="item.id"
        class="grid-item"
      >
        <span
          :style="Number(item.id) === Number(today) ? {
            backgroundColor: 'red',
            borderRadius: '5px',
            padding: '5px'
          } : {}"
        >{{ item.id }}</span>
        <EventItem 
          v-for="event in item.events"
          :key="event.id"
          :event="event"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.calendar-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 10px;
}

.grid-item {
  border: 1px solid #ccc;
  padding: 10px;
  text-align: center;
}
</style>