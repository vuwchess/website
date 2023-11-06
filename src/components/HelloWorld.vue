<script setup lang="ts">
defineProps<{
  msg: string
}>()
</script>

<template>
  <div class="greetings">
    <img alt="Vue logo" class="logo" src="@/assets/logo.png" width="125" height="125" />
    <h1>{{ msg }}</h1>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.2rem;
  position: relative;
}

p {
  font-size: 1.2rem;
}

.greetings {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0rem 1rem;
}

.greetings h1 {
  text-align: center;
  margin-top: 1rem;
}

img {
  border-radius: 25px;
}

@media (min-width: 1024px) {

  .greetings h1,
  .greetings p {
    text-align: left;
  }
}
</style>
