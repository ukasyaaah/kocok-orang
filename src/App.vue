<script setup>
import {  reactive } from "vue";
import ResultPage from "./pages/ResultPage.vue";
import AboutDev from "./components/AboutDev.vue";
import ListNamesPage from "./pages/ListNamesPage.vue";

const kocok = reactive({
  inputName: "",
  names: ["Ari", "Budi", "Citra", "Dewi", "Eka"],
  error: "",
  state: true,
});

function getRandomName() {
  return kocok.names[Math.floor(Math.random() * kocok.names.length)];
}

function generateResult() {
  kocok.state = false;
}

function resetApp() {
  kocok.inputName = "";
  kocok.names = [];
  kocok.error = "";
  kocok.state = true;
}
</script>

<template>
  <ListNamesPage
    v-model:error="kocok.error"
    v-model:names="kocok.names"
    v-model:input-name="kocok.inputName"
    :is-active="kocok.state"
    :generate-result="generateResult"
  />

  <ResultPage
    :isActive="!kocok.state"
    :reset-app="resetApp"
    :get-random-name="getRandomName"
  />

  <AboutDev />
</template>
