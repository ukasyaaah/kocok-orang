<script setup>
import { computed, reactive } from "vue";
import BaseLayout from "./layouts/BaseLayout.vue";
import ResultPage from "./pages/ResultPage.vue";
import AboutDev from "./components/AboutDev.vue";

const kocok = reactive({
  inputName: "",
  names: ["Ari", "Budi", "Citra", "Dewi", "Eka"],
  error: "",
  state: true,
});

const isReady = computed(() => (kocok.names.length > 1 ? true : false));

function addNameToList() {
  const name = kocok.inputName;
  if (validate(name)) {
    kocok.names.push(name);
    kocok.inputName = "";
    kocok.error = "";
  } else {
    return kocok.error;
  }
}

function deleteName(name) {
  return kocok.names.splice(name, 1);
  // return kocok.names.pop(name);
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
  <BaseLayout :vif="kocok.state">
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
            v-model="kocok.inputName"
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
          v-if="kocok.error"
        >
          {{ kocok.error }}
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
        :class="kocok.names.length > 0 ? 'flex md:block' : 'hidden'"
        class="justify-center md:items-center gap-3 mx-auto content-center mt-11 md:mt-0 max-w-sm lg:max-w-2xl flex-wrap"
      >
        <button
          v-for="(nameh, index) in kocok.names"
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

  <ResultPage
    :isActive="!kocok.state"
    :reset-app="resetApp"
    :get-random-name="getRandomName"
  />

  <AboutDev />
</template>
