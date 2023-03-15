<script setup>
import keyboard from "./components/keyboard.vue";
import Header from "./components/Header.vue";
import Table from "./components/Table.vue";
import { ref, onMounted } from "vue";

const input = ref("");

const onChange = (value) => {
  input.value = value;
};

// const onKeyPress = (key) => {
//   input.value += key.key;
//   console.log("Button", key);
//   // console.log(input);
// };

const onInputChange = (event) => {
  input.value = event.target.value;
};

const onKeyPress = (e) => {
  e.preventDefault();
  let key;
  if (e.shiftKey && e.keyCode === 186) {
    // Shift + :
    key = ":";
  } else {
    switch (e.keyCode) {
      case 219:
        key = "ʃ";
        break;
      case 8:
        key = "";
        input.value = input.value.slice(0, -1); // remove last character
        break;
      case 32:
        key = " ";
        break;
      case 221:
        key = "з";
        break;
      case 220:
        key = "œ";
        break;
      case 186:
        key = "ɟ";
        break;
      case 222:
        key = "ʎ";
        break;
      case 188:
        key = "ŋ";
        break;
      case 190:
        key = "ɲ";
        break;
      case 18:
        key = "";
        break;
      case 191:
        key = "ɯ";
        break;
      case 16 + 186:
        key = ":";
        break;
      default:
        key = String.fromCharCode(e.keyCode).toLowerCase();
        break;
    }
  }
  e.keyCode == 219 ? "ʃ" : String.fromCharCode(e.keyCode).toLowerCase();
  // e.keyCode == 13
  //   ? "{enter}"
  //   : e.keyCode == 8
  //   ? "{backspace}"
  //   : String.fromCharCode(e.keyCode).toLowerCase();
  input.value += key;
  // console.log("Button", key);
};

onMounted(() => {
  window.addEventListener("keydown", onKeyPress);
  // window.addEventListener("keydown", (e) => {
  //   e.preventDefault();
  //   // let key =
  //   //   e.keyCode == 13
  //   //     ? "{enter}"
  //   //     : e.keyCode == 8
  //   //     ? "{backspace}"
  //   //     : String.fromCharCode(e.keyCode).toLowerCase();
  //   onKeyPress(key);
  // });
});
</script>

<template>
  <div
    class="flex flex-col h-screen max-w-5xl px-10 mx-auto justify-evenly max-[425px]:p-1 max-[768px]:max-w-xl max-[768px]:justify-end"
  >
    <Header />
    <Table />
    <div class="flex gap-2 flex-col">
      <textarea
        :value="input"
        class="input sha shadow-md p-2 border-2 border-solid rounded-lg max-[768px]:text-lg text-3xl"
        @input="onInputChange"
        placeholder="saqalɯ: suruj :3"
        name="keyboard-input"
        cols="30"
        rows="5"
        @keydown="onKeyPress"
      >
      </textarea>
      <!-- <input :value="input" class="my-input" /> -->
      <keyboard @onChange="onChange" />
    </div>
  </div>
</template>

<style scoped>
.input {
  resize: none;
}
</style>
