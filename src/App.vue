<script setup>
import { ref } from 'vue'

import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import Calendar from './components/Calendar.vue'

// sample events data 
const events = ref([
{ title: 'Digital Nomads Thailand Co-work + Ice Bath + Sauna', date: '2024-12-02' },
  { title: 'Digital Nomads Thailand Co-work + Ice Bath + Sauna', date: '2024-12-02' },
  
  { title: 'BDN Drinks + Party', date: '2024-12-25' },
  { title: 'BDN Drinks + Party', date: '2024-12-30' },
]);

window.onload = function() {
        const itemToScrollTo = document.getElementById('15');
        if (itemToScrollTo) {
            const container = document.querySelector('.grid-container');
            const itemPosition = itemToScrollTo.offsetLeft;
            container.scrollTo({ left: itemPosition, behavior: 'smooth' });
        }
    }


</script>

<template>
  <header>
    
    <div class="wrapper">
      <HelloWorld msg="Digital Nomads Thailand Calendar" />
    </div>
  </header>

  <main>
    <Calendar 
    :events="events"
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
