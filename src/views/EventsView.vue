<script setup lang="ts">
import { Calendar } from 'v-calendar';
import 'v-calendar/style.css';

import { ref } from 'vue';

const selectedColor = ref('green');
</script>

<template>
    <div class="events">
        <h1 class="green">Events</h1>
        <Calendar :color="selectedColor" />
    </div>
</template>

<style scoped>
h1 {
    font-weight: 500;
    font-size: 2.6rem;
    position: relative;
    margin-bottom: 1rem;
}
</style>
