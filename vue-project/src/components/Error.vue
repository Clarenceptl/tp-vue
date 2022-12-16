<script setup>
import { inject, watch } from "vue";

const values = inject("errors");

</script>

<template>
  <div v-if="values">
    <div v-for="(items, key, index) in values" :key="index">
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
