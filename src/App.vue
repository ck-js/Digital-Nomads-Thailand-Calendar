<script setup>
import { ref } from 'vue'


import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import Calendar from './components/Calendar.vue'
import EventModal from './components/EventModal.vue'

const showModal = ref(false)
// sample events data 
const events = ref([
{ title: 'Digital Nomads Thailand Co-work + Ice Bath + Sauna', date: '2024-12-02' },
{ title: 'Digital Nomads Thailand Co-work + Ice Bath + Sauna', date: '2024-12-09' },
{ title: 'Digital Nomads Thailand Co-work + Ice Bath + Sauna', date: '2024-12-16' },
{ title: 'Digital Nomads Thailand Co-work + Ice Bath + Sauna', date: '2024-12-23' },
{ title: 'Digital Nomads Thailand Co-work + Ice Bath + Sauna', date: '2024-12-30' },
  
  
  { title: 'BDN Meetup & Drinks', date: '2024-12-05' },
  { title: 'BDN Meetup & Drinks', date: '2024-12-12' },
  { title: 'BDN Meetup & Drinks', date: '2024-12-19' },
  { title: 'BDN Meetup & Drinks', date: '2024-12-26' },
  
  
  
]);

</script>

<template>
  <header>

    
    <Teleport to="body">
      <EventModal 
      :event="events[0]"
      :show="showModal"

      />
    </Teleport>
    
       <div class="wrapper">
      
      <HelloWorld msg="Digital Nomads Thailand Calendar" />
    </div>
  </header>

  <main>
    <Calendar 
    :events="events",
    :showModal="showModal"
    />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
