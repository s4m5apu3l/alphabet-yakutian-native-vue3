<script setup>
import keyboard from "./components/keyboard.vue";
import { ref, onMounted } from "vue";

const input = ref("");

const onChange = (value) => {
  input.value = value;
};

const onKeyPress = (button) => {
  console.log("Button", button);
};

const onInputChange = (event) => {
  input.value = event.target.value;
};
</script>

<template>
  <div class="flex flex-col h-screen max-w-md mx-auto justify-evenly max-[768px]:justify-end">
    <div class="flex gap-2 flex-col">
      <input
        name="keyboard-input"
        :value="input"
        class="input"
        @input="onInputChange"
        placeholder="Tap on the virtual keyboard to start"
      />
      <keyboard @onChange="onChange" @onKeyPress="onKeyPress" :input="input" />
    </div>
  </div>
</template>

<style scoped>
.input {
  resize: vertical;
}
</style>
