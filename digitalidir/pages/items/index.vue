<template>
  <div class="container mx-10">
    <div class="flex w-1/2 justify-between items-center mb-6">
      <h2 class="text-2xl font-semibold">Items</h2>
      <nuxt-link
        to="/items/add"
        class="p-1.5 bg-green-600 text-white font-medium rounded-md"
      >
        Add New
      </nuxt-link>
    </div>
    <table
      class="w-1/2 border-collapse border border-gray-200 bg-white shadow-md rounded-md"
    >
      <thead class="bg-gray-100">
        <tr>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Name
          </th>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Amount
          </th>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Price
          </th>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Image
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in items"
          :key="item._id"
          class="hover:bg-gray-50 cursor-pointer"
        >
          <td class="px-4 py-2 border border-gray-300">{{ item.name }}</td>
          <td class="px-4 py-2 border border-gray-300">{{ item.amount }}</td>
          <td class="px-4 py-2 border border-gray-300">{{ item.price }}</td>

          <td class="px-4 py-2 border border-gray-300">
            <img
              class="w-32 h-auto rounded shadow"
              :src="`http://localhost:5000/${item.imageURL}`"
              alt="News Image"
            />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const items = ref([]);
const error = ref(null);

function formatToHumanReadable(isoDate) {
  const date = new Date(isoDate);

  const options = {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
    hour: 'numeric',
    minute: '2-digit',
    hour12: true,
  };

  return date.toLocaleString('en-US', options);
}

onMounted(async () => {
  try {
    console.log(localStorage.getItem('accessToken'));
    const response = await fetch(
      'http://localhost:5000/api/v1/items',

      {
        method: 'GET',
        headers: {
          Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
        },
      }
    );

    const data = await response.json();
    items.value = data;
  } catch (err) {
    console.error('Unexpected Error:', err);
  }
});
</script>

<style scoped></style>
