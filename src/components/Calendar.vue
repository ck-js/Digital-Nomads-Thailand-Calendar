<script setup>
const props = defineProps({
    events: {
        type: Array,
        required: true,
    },
});
import {ref, computed} from 'vue'
import dayjs  from 'dayjs';

const today = ref(dayjs().format('DD'));
const currentMonth = ref(dayjs().format('MMMM'));
const currentYear = ref(dayjs().format('YYYY'));
const dayNameItems = ref(['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']);

// const gridItems = ref(Array.from({ length: 35 }, (_, i) => ({ id: i + 1 })));
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

            
<h1>{{today}} {{ currentMonth}}
    <span>{{ currentYear}}</span>
</h1>

<div class="day-name-container">
<div v-for="dayName in dayNameItems">
    {{ dayName }}
</div>
</div>
<div class="grid-container">
    <div v-for="item in gridItems"
    :key="item.id"
    class="grid-item">
        <span>{{ item.id }}</span>
        <div class="event-green">{{ item.title }}</div>
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
  padding: 10px;
}
.event-green {
  background-color: hsla(160, 100%, 37%, 1);
  color: black;
  
  
  
}
.event-green:hover {
    cursor: pointer;
}
 
</style>