<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <h1 class="green">Welcome</h1>
    <p>
      This is the official website of the Victoria University of Wellington Chess Club.
    </p>
    <p>
      Here are some resources to help you connect with the club:
    </p>
    <TheWelcome />
  </main>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
}

p {
  font-size: 1.2rem;
}
</style>
