<script setup>
import {ref, computed} from 'vue'
import dayjs  from 'dayjs';

const today = ref(dayjs().format('YYYY-MM-DD'));
const currentMonth = ref(dayjs().format('MMMM'));
const currentYear = ref(dayjs().format('YYYY'));
</script>
<template>
    <header>
        <div class="wrapper">
        <h1>
            {{ today}}
            {{ currentMonth}}
            {{ currentYear}}
         </h1>
        </div>
    </header>
    
</template>