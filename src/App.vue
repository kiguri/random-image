<script setup lang="ts">
import { ref, computed } from "vue";
const width = ref(500);
const height = ref(500);
const randomNumber = ref(0);
const seed = ref("");

// computed url
const url = computed(() => {
  return `https://picsum.photos/seed/${seed.value}/${width.value}/${height.value}?random=${randomNumber.value}`;
});

// shufle the image
const shuffle = () => {
  const random = Math.floor(Math.random() * 10000);

  // random string
  const randomString =
    Math.random().toString(36).substring(2, 15) +
    Math.random().toString(36).substring(2, 15);

  seed.value = randomString;
  randomNumber.value = random;
};

// on submit
const onSubmit = (e: Event) => {
  e.preventDefault();
  shuffle();
};
</script>

<template>
  <div
    class="min-w-screen min-h-screen flex flex-col items-center justify-center gap-10"
  >
    <form class="border shadow-lg rounded-lg w-[500px] p-10" @submit="onSubmit">
      <div class="grid grid-cols-2 gap-4">
        <label class="text-gray-700">Width</label>
        <input
          type="number"
          v-model="width"
          class="border border-gray-400 p-2 w-full"
        />
        <label class="text-gray-700">Height</label>
        <input
          type="number"
          v-model="height"
          class="border border-gray-400 p-2 w-full"
        />
      </div>
      <button
        type="submit"
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
      >
        Shuffle
      </button>
    </form>

    <div class="w-[500px] h-[500px]">
      <img
        :src="url"
        class="w-full h-full rounded-lg shadow-lg object-contain"
        alt="random image"
      />
    </div>
  </div>
</template>

<style></style>
