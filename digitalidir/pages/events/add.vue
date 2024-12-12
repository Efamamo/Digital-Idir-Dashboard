<template>
  <div class="max-w-xl mx-auto shadow-md rounded-md p-10 mt-8 md:mt-40">
    <h3 class="text-center text-2xl font-bold">Add Event</h3>
    <form v-on:submit.prevent="handleSubmit">
      <div class="flex flex-col gap-2 mb-4">
        <label for="title">Title</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="text"
          id="title"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="start">Start Time</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="datetime-local"
          id="start"
         
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="start">End Time</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="datetime-local"
          id="start"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label>Description</label>
        <textarea
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
        ></textarea>
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
  title: 'DigitalIdir | Add Event',
});

const handleSubmit = () => {};
</script>

<style scoped></style>
