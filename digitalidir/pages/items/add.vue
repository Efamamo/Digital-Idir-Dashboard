<template>
  <div class="max-w-xl mx-auto shadow-md rounded-md p-10 mt-8 md:mt-40">
    <h3 class="text-center text-2xl font-bold">Add Item</h3>
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
        <label for="price">Price</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="number"
          id="price"
          v-model="price"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="amount">Amount</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="number"
          id="amount"
          v-model="amount"
        />
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
const price = ref(0);
const amount = ref(0);
const image = ref(null);

const handleFileChange = (event) => {
  const file = event.target.files[0];
  if (file) {
    image.value = file;
  }
};

useHead({
  title: 'DigitalIdir | Add Item',
});

const handleSubmit = async () => {
  const formData = new FormData();
  formData.append('name', name.value);
  formData.append('price', price.value);
  formData.append('amount', amount.value);
  if (image.value) {
    formData.append('image', image.value);
  }

  try {
    const response = await fetch('http://localhost:5000/api/v1/items', {
      method: 'POST',
      body: formData,
      headers: {
        Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
      },
    });

    if (response.ok) {
      window.location.href = '/items';
    } else {
      const data = await response.json();
      console.error('Failed to add news:', data);
    }
  } catch (e) {
    console.error(e);
  }
};
</script>

<style scoped></style>
