<script setup>
const props = defineProps({
    events: {
        type: Array,
        required: true,
    },
});
import {ref, computed, onMounted, onUnmounted, watch} from 'vue'
import dayjs  from 'dayjs';
import EventItem from './EventItem.vue'

const today = ref(dayjs());
// const previousMonth = ref(dayjs().subtract(1, 'month').format('MMMM'));
// const currentMonth = ref(dayjs());
const  isCurrentMonth = ref(today.value.format('MM') === dayjs().format('MM'));

const staticToday = dayjs()
const staticCurrentMonth = dayjs().format('MM')

// const currentYear = ref(dayjs());
const dayNameItems = ref(['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']);

// pagination control functions
const previousMonth = () => {
    today.value = today.value.subtract(1, 'month');
    
    
}
const nextMonth = () => {
  today.value = today.value.add(1, 'month');
}
const currentMonth = () => {
today.value = dayjs()

}

const preGridItems = computed(() => {
// get the first day of the month name
const firstDayOfMonth = today.value.date(1).day();
return Array.from({ length: firstDayOfMonth }, (_, i) => ({ }));

})
// const gridItems = ref(Array.from({ length: 35 }, (_, i) => ({ id: i + 1 })));
const gridItems = computed(() => {
  const daysInMonth = today.value.daysInMonth();
  
  return Array.from({ length: daysInMonth }, (_, i) => {
    const date = today.value.date(i + 1).format('YYYY-MM-DD');
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
scrollToItem(today.value.format('D'));
// alert(today.value.format('D'))

})


onUnmounted(() => {
window.removeEventListener('resize', handleResize);
})
    

    const gridContainerRef = ref(null);

    const scrollToItem = (itemId) => {
      const itemToScrollTo = document.getElementById(itemId);
      if (itemToScrollTo) {
itemToScrollTo.scrollIntoView({ behavior: 'smooth',

 });

      }
    };
    const getItemStyle = (item) => {
  return Number(item.id) === Number(today.value.format('DD')) && isCurrentMonth.value ? {
    backgroundColor: 'red',
    borderRadius: '5px',
    padding: '5px'
  } : {};
};

    watch(today, (newValue) => {
      isCurrentMonth.value = newValue.format('MM') === dayjs().format('MM');
      
    });
    

</script>
<template>
   
<h1>
    <span style="font-size: 3rem;
    font-weight: 600"
    >{{ staticToday.format('DD')}}</span> {{staticToday.format('MMMM')}}
<span>{{staticToday.format('YY')}}</span>
</h1>
<div class="pagination-controls-container">
    <button
    @click="previousMonth"
    >{{ today.subtract(1,'month').format('MMMM') }}</button>
    <h2>
        {{ today.format('MMMM') }}
    </h2>
    <!-- <button
    @click="currentMonth"
    >{{ today.format('MMMM') }}
  </button> -->
    <button
    @click="nextMonth"
    >{{ today.add(1, 'month').format('MMMM') }}</button>


</div>
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
<div 
v-if="isWideScreen"
v-for="item in preGridItems"
class="grid-item">
    <span >{{ item.id }}</span>
</div>
    <div v-for="item in gridItems"
    :key="item.id"
    :id="item.id"
    class="grid-item"
    
    >
        <span
:style="getItemStyle(item)"
        >{{ item.id }}</span>


<EventItem 
v-for="event in item.events"
:key="event.title"
:event="event"/>


</div>

            
</div>    



</template>
<style scoped>
:root {
    --green-color:  hsla(160, 100%, 37%, 1);
    --dark-green-color: hsla(160, 100%, 27%, 1);
}

.grid-container,
.day-name-container {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 1rem;
    
}
.day-name-container {
margin: 15px 0;


}
.grid-item {
  width: 100px;
  height: 100px;
}
.pagination-controls-container {
    display: flex;
    justify-content: space-between;
    margin-bottom: 15px;
    height: 50px;
    

}
.pagination-controls-container button {
  
  background-color: var(--dark-green-color);
  color: white;
  border: 1px solid var(--green-color);
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.pagination-controls-container button:hover {
  background-color: var(--green-color);
}


@media (max-width: 768px) {
    .grid-container{
        display: flex;
    flex-direction: row;    
    white-space: nowrap;
overflow-x: auto;  
scroll-snap-type-x: mandatory;
height: 100vh;
width: 100%;
    }
    
    
    .grid-item {
      flex: 0 0 150px;
      height: 100vh;
      scroll-snap-align: start;
      border-right: 0.5px solid rgba(255, 255, 255, 0.5);
        
    }
    .grid-item:last-child {
        border-right: none;
    }
    span {
        font-size: 2rem;
    }
}


</style>