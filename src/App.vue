<script setup lang="ts">
import { ref, computed, onMounted } from "vue";
const width = ref(500);
const height = ref(500);
const randomNumber = ref(0);
const seed = ref(
  Math.random().toString(36).substring(2, 15) +
    Math.random().toString(36).substring(2, 15)
);

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
    class="flex flex-col items-center justify-center min-h-screen gap-10 min-w-screen"
  >
    <form class="border shadow-lg rounded-lg w-[500px] p-10" @submit="onSubmit">
      <div class="grid grid-cols-2 gap-4">
        <label class="text-gray-700">Width</label>
        <input
          type="number"
          v-model="width"
          class="w-full p-2 border border-gray-400"
        />
        <label class="text-gray-700">Height</label>
        <input
          type="number"
          v-model="height"
          class="w-full p-2 border border-gray-400"
        />
      </div>
      <button
        type="submit"
        class="px-4 py-2 font-bold text-white bg-blue-500 rounded hover:bg-blue-700"
      >
        Shuffle
      </button>
    </form>

    <div class="w-[500px] h-[500px]">
      <img
        :src="url"
        class="object-contain w-full h-full rounded-lg shadow-lg"
        alt="random image"
      />
    </div>
  </div>
</template>

<style></style>
