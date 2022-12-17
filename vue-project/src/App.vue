<script setup>
import Field from "./components/Field.vue";
import Formik from "./components/Formik.vue";
import Error from "./components/Error.vue";
import { reactive } from "vue";

const options = [
  { value: "1", label: "Option 1" },
  { value: "2", label: "Option 2" },
  { value: "3", label: "Option 3" },
];
const initialValues = reactive({
  email: "",
  password: "",
  select: "3",
});

const submit = (values) => {
  console.log(values, "submit fonction");
  initialValues.email = "";
  initialValues.password = "";
  initialValues.select = "";
};

const validate = (values) => {
  const errors = {};
  if (!values.email) {
    errors.email = "Required";
  } else if (!/\S+@\S+\.\S+/.test(values.email)) {
    errors.email = "Invalid email address";
  }
  return errors;
};
</script>

<template>
  <header>
    <h1>Formikado</h1>
  </header>

  <main class="container">
    <Formik
      :initial-values="initialValues"
      :on-submit="submit"
      :validate="validate"
    >
      <Field type="notValid" name="Totoo" />
      <Field type="email" name="email" />
      <Field type="password" name="password" />
      <Field type="select" name="select">
        <option v-for="option in options" :value="option.value">
          {{ option.label }}
        </option>
      </Field>
      <Error />
      <template v-slot:button="{ submitForm }">
        <button type="submit" @click="submitForm">Submit</button>
      </template>
    </Formik>
  </main>
</template>

<style>
.header {
  background-color: #f1f1f1;
  padding: 30px;
  text-align: center;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
