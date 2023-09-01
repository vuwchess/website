<script setup lang="ts">
defineProps<{
  msg: string
}>()
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <p>
      This is the official website of the Victoria University of Wellington Chess Club.
    </p>
    <p>
      Here are some resources to help you connect with the club:
    </p>
  </div>
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

.greetings h1,
.greetings p {
  text-align: center;
  margin-top: 1rem;
}

@media (min-width: 1024px) {

  .greetings h1,
  .greetings p {
    text-align: left;
  }
}
</style>
