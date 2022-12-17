<script setup>
import { inputType } from "../enum";
import { inject } from "vue";
const props = defineProps({
  type: {
    type: String,
    required: true,
    default: "email",
  },
  name: {
    type: String,
    required: true,
    default: "email",
  },
});

const values = inject("formValues");

const isSelect = () => {
  return props.type === "select";
};
const isValidInput = () => {
  return inputType.includes(props.type);
};
</script>

<template>
  <div v-if="isValidInput()">
    <label :for="name">{{ name }}</label>
    <!-- Comprend pas pourquoi v-model ne marche pas ici -->
    <component
      :id="name"
      :is="isSelect() ? 'select' : 'input'"
      :type="!isSelect() ? type : null"
      :name="name"
      :value="values[type]"
      @input="(e) => (values[type] = e.target.value)"
    >
      <slot v-if="isSelect()"></slot>
    </component>
  </div>
</template>

<style scoped></style>
