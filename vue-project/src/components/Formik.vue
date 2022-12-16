<script setup>
import { provide } from "vue";
const emit = defineEmits(["submitted"]);

const props = defineProps({
  validate: {
    type: Function,
    required: true,
  },
  initialValues: {
    type: Object,
    required: false,
  },
  onSubmit: {
    type: Function,
    required: true,
  },
});

provide("formValues", props.initialValues);
const handleSubmit = (e) => {
  e.preventDefault();
  const errors = props.validate(props.initialValues);
  if (Object.keys(errors).length === 0) {
    props.onSubmit(props.initialValues);
  } else {
    console.log(errors, "errors");
  }
};
</script>

<template>
  <form action="">
    <slot></slot>
    <slot name="button" :submit-form="handleSubmit"></slot>
  </form>
</template>
