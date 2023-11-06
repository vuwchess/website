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
  margin-top: 4rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
