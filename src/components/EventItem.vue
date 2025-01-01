<script setup>

import { ref } from 'vue'
import EventModal from './EventModal.vue';
const props = defineProps({
  event: {
    type: Object,
    required: true
  },

});
const showModal = ref(false)

</script>


<template>
  
  <div :class="['event-item', event.label ? `${event.label}` : '']">
    
    <h6>
      <button
      @click="showModal = true"
      >  
      {{ event.title }}
    </button>
    </h6>
  
  </div>
<EventModal
:event="event"
:show="showModal"
@close="showModal = false"
/>  
  

</template>


<style scoped>
button {
  background: none;
  border: none;
  padding: 0;
  width: 100%;
  height: 100%;
  font: inherit;
  cursor: pointer;
  outline: inherit;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.event-item {
  color: black;
  
  margin-top: 5px;
  padding: 5px;
  border-radius: 3px;
cursor: pointer;
}
h6,
button {
  
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.green {
  background-color: hsla(160, 100%, 37%, 1);
  
}
.turquoise{
  background-color: turquoise;
}

@media (max-width: 768px) {
  button {
    height: 100px;
padding-bottom: 80%;
    
    

    


    
  }
}
</style>






