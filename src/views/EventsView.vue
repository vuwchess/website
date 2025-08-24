<script setup lang="ts">
import EventGallery from '@/components/EventGallery.vue';
import 'v-calendar/style.css';
</script>

<template>
    <div class="events">
        <h1 class="green">Events</h1>
        <EventGallery />
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
