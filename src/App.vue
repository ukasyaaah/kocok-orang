<script setup>
import { reactive } from "vue";

const kocok = reactive({
  inputName: "",
  names: ["ari", "arfi"],
  error: "",
});

function addNameToList() {
  const name = kocok.inputName;
  if (validate(name)) {
    kocok.names.push(name);
    kocok.inputName = "";
  } else {
    return kocok.error;
  }
}

function validate(value) {
  if (!value) {
    kocok.error = "Nama Ga Boleh Kosong!";
    return false;
  } else if (kocok.names.includes(value)) {
    kocok.error = "Nama Ga Boleh Sama!";
    return false;
  } else {
    return true;
  }
}
</script>

<template>
  <h1>Kocok Orang</h1>
  <form class="input-form">
    <input type="text" v-model="kocok.inputName" />
    <button @click.enter.prevent="addNameToList">Tambah</button>
  </form>
  <h3 v-if="kocok.error">
    {{ kocok.error }}
  </h3>
  <button v-for="nameh in kocok.names">
    {{ nameh }}
  </button>

</template>

<style scoped>
.input-form {
  margin: 0;

  button {
    border: 2px solid black;
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
  }

  input {
    padding: 11.3px;
    border: 2px solid black;
    border-top-left-radius: 12px;
    border-bottom-left-radius: 12px;
  }
}
</style>
