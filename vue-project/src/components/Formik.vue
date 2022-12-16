<script setup>
import { provide, reactive } from "vue";

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

let error = reactive([]);
provide("errors", error);

const handleSubmit = (e) => {
  e.preventDefault();
  if (error.length > 0) error.pop();
  const errors = props.validate(props.initialValues);
  if (Object.keys(errors).length === 0) {
    props.onSubmit(props.initialValues);
  } else {
    error.push(errors);
  }
};
</script>

<template>
  <form action="">
    <slot></slot>
    <slot name="button" :submit-form="handleSubmit"></slot>
  </form>
</template>
