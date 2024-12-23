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


<template>
  <div class="event-green">
    <h6>{{ event.title }}</h6>
  </div>
</template>

<script setup>
const props = defineProps({
  event: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>
h6 {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.event-green {
  background-color: hsla(160, 100%, 37%, 1);
  color: black;
  height: 20%;
  margin-top: 5px;
}
</style>