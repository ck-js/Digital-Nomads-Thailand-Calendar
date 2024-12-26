<script setup>
const props = defineProps({
    events: {
        type: Array,
        required: true,
    },
});
import {ref, computed, onMounted, onUnmounted} from 'vue'
import dayjs  from 'dayjs';
import EventItem from './EventItem.vue'


const today = ref(dayjs().format('DD'));
const currentMonth = ref(dayjs().format('MMMM'));
const currentYear = ref(dayjs().format('YYYY'));
const dayNameItems = ref(['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']);

const preGridItems = computed(() => {
// get the first day of the month name
const firstDayOfMonth = dayjs().date(1).day() +2;
return Array.from({ length: firstDayOfMonth }, (_, i) => ({ }));

})

// const gridItems = ref(Array.from({ length: 35 }, (_, i) => ({ id: i + 1 })));
const gridItems = computed(() => {
  const daysInMonth = dayjs().daysInMonth();
  
    
  return Array.from({ length: daysInMonth }, (_, i) => {
    const date = dayjs().date(i + 1).format('YYYY-MM-DD');
    const dayEvents = props.events.filter(event =>
      event.date === date
    )
    // const event = props.events.find(event => event.date === date);
    
    
    return {
      id: i + 1,
      date,
      // title: event ? event.title : '',
      // events: event ? [{title: event.title}] : ''
      events: dayEvents
    };
  });
});
console.log(gridItems.value);

// dynamically conditionally render the day name container
const isWideScreen = ref(window.innerWidth > 768)

const handleResize = () => {
    isWideScreen.value = window.innerWidth > 768;
    // alert(isWideScreen.value)
}
onMounted(() => {
window.addEventListener('resize', handleResize);
// scrollToItem(today.value);

})


onUnmounted(() => {
window.removeEventListener('resize', handleResize);
})
    

    const gridContainerRef = ref(null);

    const scrollToItem = (itemId) => {
      const itemToScrollTo = document.getElementById(itemId);
      if (itemToScrollTo && scrollContainer.value) {
        const itemPosition = itemToScrollTo.offsetLeft;
        scrollContainer.value.scrollTo({ left: itemPosition, behavior: 'smooth' });
      }
    };

scrollToItem(today.value);
</script>
<template>

            
<h1>{{today}} {{ currentMonth}}
    <span>{{ currentYear}}</span>
</h1>

<div
v-if="isWideScreen" 
class="day-name-container">
<div v-for="dayName in dayNameItems">
    {{ dayName }}
</div>
</div>
<div class="grid-container"
ref="gridContainerRef"
>
<div v-for="item in preGridItems"
class="grid-item">
    <span>{{ item.id }}</span>
</div>
    <div v-for="item in gridItems"
    :key="item.id"
    :id="item.id.toString()"
    class="grid-item"
    :class="{ today: item.id === today }"
    
    >
        <span
        :style="Number(item.id) === Number(today) ? {backgroundColor: 'red',
            borderRadius: '50%', padding: '5px'
        } : {}"
        >{{ item.id }}</span>
        
<div
v-for="event in item.events"
:key="event.title"
class="event-green">
{{ event.title }}
</div> -->
<EventItem 
v-for="event in item.events"
:key="event.title"
:event="event"/>



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
.event-green {
background-color: hsla(160, 100%, 37%, 1);
  color: black;
  height: 20%;
  
  
}
.event-green:hover {
    cursor: pointer;
}

@media (max-width: 768px) {
    .grid-container{
        display: flex;
    flex-direction: row;    
    white-space: nowrap;
overflow-x: auto;  
/* scroll-snap-type-x: mandatory; */
height: 100vh;
width: 100%;
    }
    
    
    .grid-item {
      flex: 0 0 150px;
      height: 100vh;
      /* scroll-snap-align: start; */
        
    }
    span {
        font-size: 2rem;
    }
}


</style>