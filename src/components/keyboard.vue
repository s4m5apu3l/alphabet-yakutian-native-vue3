<script setup>
import { ref, onMounted, watch } from "vue";
import Keyboard from "simple-keyboard";
import "simple-keyboard/build/css/index.css";

const keyboard = ref(null);

const emit = defineEmits(["onKeyPress", "onChange"]);

const props = defineProps({
  keyboardClass: {
    default: "simple-keyboard",
    type: String,
  },
  input: {
    type: String,
  },
});

const onChange = (input) => {
  emit("onChange", input);
};
const onKeyPress = (button) => {
  emit("onKeyPress", button);

  if (button === "{shift}" || button === "{lock}") handleShift();
  if (button === "{numbers}" || button === "{abc}") handleNumbers();
  if (button === "{ent}")  clear();
};

const handleShift = () => {
  let currentLayout = keyboard.value.options.layoutName;
  let shiftToggle = currentLayout === "default" ? "shift" : "default";

  keyboard.value.setOptions({
    layoutName: shiftToggle,
  });
};

function handleNumbers() {
  let currentLayout = keyboard.value.options.layoutName;
  let numbersToggle = currentLayout !== "numbers" ? "numbers" : "default";

  keyboard.value.setOptions({
    layoutName: numbersToggle,
  });
}

function clear() {
  keyboard.value.clearInput()
}

onMounted(() => {
  keyboard.value = new Keyboard(props.keyboardClass, {
    onChange: onChange,
    onKeyPress: onKeyPress,
    layout: {
      default: [
        
        "q w e r t y u i o p",
        "a s d f g h j k l",
        "{shift} з x c ʃ b n m {backspace}",
        "{numbers} {space} {ent}",
      ],
      shift: [
        "Q W E R T Y U I O P",
        "A S D F G H J K L",
        "{shift} Z X C V B N M {backspace}",
        "{numbers} {space} {ent}",
      ],
      numbers: ["1 2 3", "4 5 6", "7 8 9", "{abc} 0 {backspace}"],
    },
    display: {
      "{space}": " Пробел",
      "{numbers}": "123",
      "{ent}": "Очистить",
      "{escape}": "esc ⎋",
      "{tab}": "tab ⇥",
      "{backspace}": "⌫",
      "{capslock}": "caps lock ⇪",
      "{shift}": "⇧",
      "{controlleft}": "ctrl ⌃",
      "{controlright}": "ctrl ⌃",
      "{altleft}": "alt ⌥",
      "{altright}": "alt ⌥",
      "{metaleft}": "cmd ⌘",
      "{metaright}": "cmd ⌘",
      "{abc}": "ABC",
    },
  });
});

</script>

<template>
  <div :class="keyboardClass"></div>
</template>

<style scoped></style>
