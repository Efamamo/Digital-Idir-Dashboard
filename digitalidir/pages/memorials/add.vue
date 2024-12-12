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
          v-model="name"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="dob">Date of Birth</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="date"
          id="dob"
          v-model="dob"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="dop">Date of Passing</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="date"
          id="dop"
          v-model="dop"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label>Description</label>
        <textarea
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          v-model="desc"
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
const name = ref('');
const dob = ref(null);
const dop = ref(null);
const image = ref(null);
const desc = ref(null);

const handleFileChange = (e) => {
  const file = e.target.files[0];
  if (file) {
    image.value = file;
  }
};
useHead({
  title: 'DigitalIdir | Add Memorial',
});

const handleSubmit = async () => {
  const formData = new FormData();
  formData.append('name', name.value);
  formData.append('dateOfBirth', dob.value);
  formData.append('dateOfPassing', dop.value);
  formData.append('description', desc.value);

  if (image.value) {
    formData.append('image', image.value);
  }

  try {
    const response = await fetch('http://localhost:5000/api/v1/memorials', {
      method: 'POST',
      body: formData,
      headers: {
        Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
      },
    });

    if (response.ok) {
      window.location.href = '/memorials';
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
