<script setup>
import BaseLayout from "../layouts/BaseLayout.vue";


const { isActive, resetApp, getRandomName } = defineProps([
  "isActive",
  "resetApp",
  "getRandomName",
]);
</script>

<template>
  <BaseLayout :vif="isActive">
    <div class="flex flex-col justify-around h-70 items-center">
      <h1 class="text-xl font-semibold">Pemenangnya adalah</h1>
      <p class="text-9xl text-tahiti font-bold">{{ getRandomName() }}!</p>
      <button @click="resetApp" class="button">Mulai Lagi</button>
    </div>
  </BaseLayout>
</template>
