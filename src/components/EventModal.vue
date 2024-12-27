<script setup>
import { ref, defineProps } from 'vue'
// modal contents
const props = defineProps({
    event: {
        type: Object,
        
    },
    show: {
        type: Boolean,
        required: true,
    }
})

</script>

<template>

<Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-container">
        <div class="modal-header">
          <slot name="header">{{ props.event.title }}</slot>
        </div>

        <div class="modal-body">
          <slot name="body">default body</slot>
        </div>

        <div class="modal-footer">
          <slot name="footer">
            default footer
            <button
              class="modal-default-button"
              @click="$emit('close')"
            >OK</button>
          </slot>
        </div>
      </div>
    </div>
  </Transition>
    



</template>

