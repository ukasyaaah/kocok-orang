<script setup>
import AboutDev from '../components/AboutDev.vue';

defineProps({
  vif: Boolean,
});
</script>

<template>
  <AboutDev/>
  <div
    v-if="vif"
    class="animate__animated animate__bounceInUp h-screen justify-center items-center mx-auto flex"
  >
    <slot />
  </div>
</template>
