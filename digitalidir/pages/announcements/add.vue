<template>
  <div class="max-w-xl mx-auto shadow-md rounded-md p-10 mt-8 md:mt-40">
    <h3 class="text-center text-2xl font-bold">Add Announcement</h3>
    <form v-on:submit.prevent="handleSubmit">
      <div class="flex flex-col gap-2 mb-4">
        <label for="title">Title</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="text"
          id="title"
          v-model="title"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label>Description</label>
        <textarea
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          v-model="description"
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
const title = ref('');
const description = ref('');
useHead({
  title: 'DigitalIdir | Add Announcement',
});

const handleSubmit = async () => {
  try {
    const response = await fetch('http://localhost:5000/api/v1/announcements', {
      method: 'POST',
      body: JSON.stringify({
        title: title.value,
        description: description.value,
      }),
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
      },
    });

    if (response.ok) {
      window.location.href = '/announcements';
    } else {
      const data = await response.json();
      console.log(data);
    }
  } catch (e) {
    console.error(e);
  }
};
</script>

<style scoped></style>
