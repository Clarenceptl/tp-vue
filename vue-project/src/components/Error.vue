<script setup>
import { inject } from "vue";

const values = inject("errors");

</script>

<template>
  <div v-if="values">
    <div v-for="(items, index) in values" :key="index">
      <p class="error" v-for="(elem, i) in items" :key="index">
        {{ i }} : {{ elem }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.error {
  color: red;
}
</style>
