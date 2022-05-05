<template>
  <input
    class="input"
    :class="{
      inputOngoing: inputOngoing,
      inputError: inputError,
      inputValid: inputValid,
    }"
    @focus="
      input.focus = true;
      input.touched = true;
    "
    @blur="input.focus = false"
    type="text"
    v-model="input.value"
  />
</template>

<script setup lang="ts">
import { reactive, computed } from "vue";

const input = reactive({
  value: "",
  focus: false,
  touched: false,
});

const inputOngoing = computed(() => input.focus && input.value.length);
const inputError = computed(
  () => !input.focus && input.touched && input.value.length < 5
);
const inputValid = computed(
  () => input.touched && !input.focus && !inputError.value
);
</script>

<style scoped>
.input {
  outline: 0px;
  border: 2px solid black;
  border-radius: 4px;
  height: 30px;
  width: 150px;
}
.inputOngoing {
  border-color: blue;
}
.inputError {
  border-color: red;
}
.inputValid {
  border-color: green;
}
</style>
