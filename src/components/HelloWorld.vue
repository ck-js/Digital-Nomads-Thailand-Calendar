<script setup>
import dntLogo from '../assets/dnt-logo-3.PNG'
defineProps({
  msg: {
    type: String,
    // required: true,
  },
})
</script>

<template>
  <div class="greetings">
    <!-- <h1 class="green">{{ msg }}</h1> -->
     <img 
     class="logo"
     :src="dntLogo" alt="Digital Nomads Thailand Logo" />
    <h3>
      The all-in-one place to discover and connect with
      <a href="https://web.facebook.com/groups/thailanddigitalnomads/?ref=share_group_link&_rdc=1&_rdr" target="_blank" rel="noopener">Digital Nomads</a>
      in Thailand.
    </h3>
  </div>
</template>

<style scoped>
.logo {
  display: block;
  margin: 0 auto 2rem;
  width: 100%;
  max-width: 300px;

  
}


h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
