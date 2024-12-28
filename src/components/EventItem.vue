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
  
  <div class="event-item green">
    
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
  font: inherit;
  cursor: pointer;
  outline: inherit;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.event-item {
  color: black;
  height: 20%;
  margin-top: 5px;
  padding: 5px;
  border-radius: 3px;

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

.event-green:hover {
  cursor: pointer;
}
</style>