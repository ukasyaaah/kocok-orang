<script setup>
defineProps({
  vif: Boolean,
});
</script>

<template>
  <div v-if="vif" class="animate__animated animate__bounceInUp h-screen justify-center items-center mx-auto flex">
    <slot />
  </div>
</template>
