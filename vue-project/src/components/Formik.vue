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

let errors = reactive([]);
provide("errors", errors);

const handleSubmit = (e) => {
  e.preventDefault();
  if (errors.length > 0) errors.splice(0, errors.length);
  const resErrors = props.validate(props.initialValues);
  if (Object.keys(resErrors).length === 0) {
    props.onSubmit(props.initialValues);
  } else {
    errors.push(resErrors);
  }
};
</script>

<template>
  <form>
    <slot></slot>
    <slot name="button" :submit-form="handleSubmit"></slot>
  </form>
</template>
