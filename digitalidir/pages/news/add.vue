<template>
  <div class="max-w-xl mx-auto shadow-md rounded-md p-10 mt-8 md:mt-40">
    <h3 class="text-center text-2xl font-bold">Add News</h3>
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

      <div class="flex flex-col gap-2 mb-4">
        <label for="image">Image</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="file"
          id="image"
          @change="handleFileChange"
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
const title = ref('');
const description = ref('');
const image = ref(null);

useHead({
  title: 'DigitalIdir | Add News',
});

// Handle file input change
const handleFileChange = (event) => {
  const file = event.target.files[0];
  if (file) {
    image.value = file;
  }
};

const handleSubmit = async () => {
  const formData = new FormData();
  formData.append('title', title.value);
  formData.append('description', description.value);
  if (image.value) {
    formData.append('image', image.value);
  }

  try {
    // Send formData to backend
    const response = await fetch('http://localhost:5000/api/v1/news', {
      method: 'POST',
      body: formData,
      headers: {
        Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
      },
    });

    if (response.ok) {
      const result = await response.json();
      window.location.href = '/news';
    } else {
      console.error('Failed to add news:', response.body);
    }
  } catch (error) {
    console.error('Unexpected Error:', error);
  }
};
</script>

<style scoped></style>
