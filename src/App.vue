<script setup>
import keyboard from "./components/keyboard.vue";

const handleInput = (key) => {
  console.log(key)
}
</script>

<template>
  <div class="flex flex-col h-screen max-w-md mx-auto justify-evenly">
    <keyboard @onKeyPress="handleInput"/>
  </div>
</template>

<style scoped></style>
