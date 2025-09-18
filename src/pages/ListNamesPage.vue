<script setup>
import { computed } from "vue";
import BaseLayout from "../layouts/BaseLayout.vue";

const { isActive, generateResult } = defineProps([
  "isActive",
  "generateResult",
]);

const inputName = defineModel("inputName");
const error = defineModel("error");
const names = defineModel("names");
const isReady = computed(() => (names.value.length > 1 ? true : false));

function addNameToList() {
  const name = inputName.value;
  if (validate(name)) {
    names.value.push(name);
    inputName.value = "";
    error.value = "";
  } else {
    return error.value;
  }
}

function validate(value) {
  if (!value) {
    error.value = "Nama Ga Boleh Kosong!";
    return false;
  } else if (names.value.includes(value)) {
    error.value = "Nama Ga Boleh Sama!";
    return false;
  } else {
    return true;
  }
}

function deleteName(name) {
  return names.value.splice(name, 1);
  // return kocok.names.pop(name);
}
</script>

<template>
  <BaseLayout :vif="isActive">
    <div class="md:flex mx-5 md:gap-20 items-center lg:gap-40">
      <div
        :class="isReady ? 'h-90' : 'h-70'"
        class="flex flex-col justify-around shadow-2xl shadow-tahiti items-center max-w-sm md:max-w-md mx-auto p-15 rounded-2xl bg-tahiti text-teks"
      >
        <h1 class="font-bold text-3xl">Kocok Orang</h1>
        <form class="flex gap-x-4 justify-center">
          <input
            class="border focus:outline-teks rounded-lg"
            type="text"
            v-model="inputName"
          />
          <button
            class="hover:cursor-pointer button"
            @click.enter.prevent="addNameToList"
          >
            Tambah
          </button>
        </form>
        <h3
          class="animate__animated animate__wobble font-bold text-lg"
          v-if="error"
        >
          {{ error }}
        </h3>

        <button
          class="button animate__animated animate__fadeInDown"
          @click.prevent="generateResult"
          v-if="isReady"
        >
          Kocok Sekarang!
        </button>
      </div>

      <div
        :class="names.length > 0 ? 'flex md:block' : 'hidden'"
        class="justify-center md:items-center gap-3 mx-auto content-center mt-11 md:mt-0 max-w-sm lg:max-w-2xl flex-wrap"
      >
        <button
          v-for="(nameh, index) in names"
          @click.prevent="deleteName(index)"
          :key="index"
          class="button md:m-3 animate__animated animate__bounceInUp"
        >
          <p>
            {{ nameh }}
          </p>
        </button>
      </div>
    </div>
  </BaseLayout>
</template>
