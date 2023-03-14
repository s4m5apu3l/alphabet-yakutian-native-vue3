<script setup>
import keyboard from "./components/keyboard.vue";
import Header from "./components/Header.vue";
import Table from "./components/Table.vue";
import { ref, onMounted } from "vue";

const input = ref("");

const onChange = (value) => {
  input.value = value;
};

const onKeyPress = (key) => {
  console.log("Button", key);
};

const onInputChange = (event) => {
  input.value = event.target.value;
};

onMounted(() => {
  window.addEventListener("keyup", (e) => {
    e.preventDefault();
    let key =
      e.keyCode == 13
        ? "{enter}"
        : e.keyCode == 8
        ? "{backspace}"
        : String.fromCharCode(e.keyCode).toLowerCase();
    onKeyPress(key);
  });
});
</script>

<template>
  <div
    class="flex flex-col h-screen max-w-5xl px-10 mx-auto justify-evenly max-[425px]:p-1 max-[768px]:max-w-xl max-[768px]:justify-end"
  >
    <Header />
    <Table />
    <div class="flex gap-2 flex-col">
      <!-- <textarea
        :value="input"
        class="input sha shadow-md p-2 border-2 border-solid rounded-lg max-[768px]:text-lg text-3xl"
        @input="onInputChange"
        placeholder="saqalɯ: suruj :3"
        name="keyboard-input"
        cols="30"
        rows="5"
      >
      </textarea> -->
      <input :value="input" class="my-input" />
      <keyboard @onChange="onChange" @onKeyPress="onKeyPress"  />
    </div>
  </div>
</template>

<style scoped>
.input {
  resize: none;
}
</style>
