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




<template>
  <div class="calendar-container" ref="calendarContainer">
    <div
      v-for="(item, index) in items"
      :key="index"
      class="calendar-item"
      :class="{ today: isToday(item) }"
    >
      {{ item }}
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  setup() {
    const items = ref(Array.from({ length: 30 }, (_, i) => new Date(2023, 11, i + 1).toLocaleDateString())); // Example dates for December 2023
    const calendarContainer = ref(null);

    const isToday = (date) => {
      const today = new Date();
      return new Date(date).toDateString() === today.toDateString();
    };

    const scrollToToday = () => {
      const todayIndex = items.value.findIndex(item => isToday(item));
      if (todayIndex !== -1 && calendarContainer.value) {
        const itemWidth = calendarContainer.value.children[todayIndex].offsetWidth;
        const scrollLeft = itemWidth * todayIndex;
        calendarContainer.value.scrollTo({ left: scrollLeft, behavior: 'smooth' });
      }
    };

    onMounted(() => {
      scrollToToday();
    });

    return {
      items,
      calendarContainer,
      isToday,
    };
  },
};
</script>

<style scoped>
.calendar-container {
  display: flex;
  overflow-x: auto;
  white-space: nowrap;
}

.calendar-item {
  min-width: 100px; /* Adjust as needed */
  padding: 10px;
  border: 1px solid #ccc;
  margin: 5px;
  border-radius: 5px;
}

.today {
  background-color: yellow; /* Highlight today's item */
}
</style>