<template>
  <div class="event-item green">
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
.event-item {
  color: black;
  height: 20%;
  margin-top: 5px;
  padding: 5px;
  border-radius: 3px;

}
h6 {
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