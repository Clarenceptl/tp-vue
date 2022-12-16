<script setup>
import Field from "./components/Field.vue";
import Formik from "./components/Formik.vue";

const options = [
  { value: "1", label: "Option 1" },
  { value: "2", label: "Option 2" },
  { value: "3", label: "Option 3" },
];
const initialValues = {
  email: "test@test.com",
  password: "password",
};

const submit = (values) => {
  console.log(values);
};

const validate = (values) => {
  console.log(values);
};
</script>

<template>
  <header>
    <h1>He ça formik ou pas</h1>
  </header>

  <main class="container">
    <Formik
      v-slot="slotProps"
      :initial-values="initialValues"
      :on-submit="submit"
      :validate="validate"
    >
      <Field type="email" name="email" />
      <Field type="password" name="password" />
      <button type="submit">Submit</button>
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
