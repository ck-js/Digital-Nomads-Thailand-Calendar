<template>
  <div class="event-green">
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

h6 {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.event-green {
  background-color: hsla(160, 100%, 37%, 1);
  color: black;
  height: 20%;
  margin-top: 5px;
}

.event-green:hover {
  cursor: pointer;
}
</style>