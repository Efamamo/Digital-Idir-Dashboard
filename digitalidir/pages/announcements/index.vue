<template>
  <div class="mx-10">
    <h2 class="text-2xl font-semibold mb-6">Announcements</h2>
    <table
      class="min-w-full border-collapse border border-gray-200 bg-white shadow-md rounded-md"
    >
      <thead class="bg-gray-100">
        <tr>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Title
          </th>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Description
          </th>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Date
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="announcement in announcements"
          :key="announcement._id"
          class="hover:bg-gray-50 cursor-pointer"
        >
          <td class="px-4 py-2 border border-gray-300">
            {{ announcement.title }}
          </td>
          <td class="px-4 py-2 border border-gray-300">
            {{ announcement.description }}
          </td>
          <td class="px-4 py-2 border border-gray-300">
            {{ formatToHumanReadable(announcement.date) }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const announcements = ref([]);
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
    const response = await fetch(
      'http://localhost:5000/api/v1/announcements',

      {
        method: 'GET',
        headers: {
          Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
        },
      }
    );

    const data = await response.json();
    console.log(data);
    announcements.value = data;
  } catch (err) {
    console.error('Unexpected Error:', err);
  }
});
</script>

<style scoped></style>
