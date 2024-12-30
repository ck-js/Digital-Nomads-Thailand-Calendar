<script setup>
import { ref,  } from 'vue'
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
const emits = defineEmits(['close'])
</script>

<template>

<Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-container">
        <div class="modal-header">
          <slot name="header">{{ props.event.title }}</slot>
        </div>

        <div class="modal-body">
          <slot name="body">
            <p>
{{ props.event.description }}
</p>

          </slot>
        </div>

        <div class="modal-footer">
          <slot name="footer">
            <a href="https://facebook.com/events/s/digital-nomads-meetup-bangkok/896696342619397/?">
                {{ props.event.link }}
            </a>
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

<style>
:root {
    --green-color:  hsla(160, 100%, 37%, 1);
}


.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  transition: opacity 0.3s ease;
}

.modal-container {
  width: 600px;
  margin: auto;
  padding: 20px 30px;
  background-color: black;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  /* border: 1px solid yellow; */
}

.modal-header h3 {
  margin-top: 0;
  
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
  background-color: var(--green-color);
  border: none;
  outline: none;
  padding: 5px 10px;
  border-radius: 2px;
  cursor: pointer;

}


/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
