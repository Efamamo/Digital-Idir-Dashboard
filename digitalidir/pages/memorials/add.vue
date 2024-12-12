<template>
  <div class="max-w-xl mx-auto shadow-md rounded-md p-10 mt-8 md:mt-40">
    <h3 class="text-center text-2xl font-bold">Add Memorial</h3>
    <form v-on:submit.prevent="handleSubmit">
      <div class="flex flex-col gap-2 mb-4">
        <label for="name">Name</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="text"
          id="name"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="dob">Date of Birth</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="date"
          id="dob"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="dot">Date of Passing</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="date"
          id="dot"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label>Description</label>
        <textarea
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
        ></textarea>
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="image">Image</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="file"
          id="image"
        />
      </div>

      <button
        type="submit"
        class="w-full bg-blue-500 p-1.5 mt-4 text-white font-semibold rounded-sm"
      >
        Add
      </button>
    </form>
  </div>
</template>

<script setup>
useHead({
  title: 'DigitalIdir | Add Memorial',
});

const handleSubmit = () => {};
</script>

<style scoped></style>
