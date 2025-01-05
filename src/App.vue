<script setup>
import { ref } from 'vue'


import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import Calendar from './components/Calendar.vue'
import EventModal from './components/EventModal.vue'
import {Event} from './event.js'
import {Event2} from './Event2.js'
import {Event3} from './Event3.js'


// sample events data 
const events = ref([
new Event('2024-12-02', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),
new Event('2024-12-09', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),
new Event('2024-12-16', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),
new Event('2024-12-23', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),
new Event('2024-12-30', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),


  new Event('2025-01-06', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),
  new Event('2025-01-13', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),
  new Event('2025-01-20', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),
  new Event('2025-01-27', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),

new Event2('2025-01-03', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),
new Event2('2025-01-06', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),
new Event2('2025-01-09', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),
new Event2('2025-01-12', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),
new Event2('2025-01-15', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),
new Event2('2025-01-18', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),
new Event2('2025-01-21', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),
new Event2('2025-01-24', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),
new Event2('2025-01-27', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),
new Event2('2025-01-30', 'https://www.facebook.com/events/s/digital-nomads-thailand-meet-u/602226502491127/'),



new Event3('2025-01-18', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),
new Event3('2025-01-19', 'https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?'),




  
]);

</script>

<template>
  <header>

    

    
       <div class="wrapper">
      
      <HelloWorld msg="Digital Nomads Thailand Calendar" />
    </div>
  </header>

  <main>
    <Calendar 
    :events="events",
    
    />
  </main>
</template>

<style scoped>
:root {
    --green-color:  hsla(160, 100%, 37%, 1);
}
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
