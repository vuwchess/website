<script setup lang="ts">
import ImageGallery from '../components/ImageGallery.vue';
</script>

<template>
  <div class="photos">
    <ImageGallery />
  </div>
</template>

<style scoped>
.photos {
  margin-top: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}
</style>
