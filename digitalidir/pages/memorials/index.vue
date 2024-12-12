<template>
  <div class="container mx-auto">
    <div class="flex w-1/2 justify-between items-center mb-6">
      <h2 class="text-2xl font-semibold">Memorials</h2>
      <nuxt-link
        to="/memorials/add"
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
            Date Of Birth
          </th>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Date Of Passing
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
          v-for="memorial in memorials"
          :key="memorial._id"
          class="hover:bg-gray-50 cursor-pointer"
        >
          <td class="px-4 py-2 border border-gray-300">
            {{ memorial.name }}
          </td>
          <td class="px-4 py-2 border border-gray-300">
            {{ formatToHumanReadable(memorial.dateOfBirth) }}
          </td>
          <td class="px-4 py-2 border border-gray-300">
            {{ formatToHumanReadable(memorial.dateOfPassing) }}
          </td>

          <td class="px-4 py-2 border border-gray-300">
            <img
              class="w-24 h-auto rounded shadow"
              :src="`http://localhost:5000/${memorial.imageUrl}`"
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

const memorials = ref([]);
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
      'http://localhost:5000/api/v1/memorials',

      {
        method: 'GET',
        headers: {
          Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
        },
      }
    );

    const data = await response.json();
    memorials.value = data;
  } catch (err) {
    console.error('Unexpected Error:', err);
  }
});
</script>

<style scoped></style>
