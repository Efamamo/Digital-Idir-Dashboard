<template>
  <div class="mx-10">
    <h2 class="text-2xl font-semibold mb-6">Users</h2>
    <table
      class="min-w-1/2 border-collapse border border-gray-200 bg-white shadow-md rounded-md"
    >
      <thead class="bg-gray-100">
        <tr>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Username
          </th>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Email
          </th>
          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          >
            Phone Number
          </th>

          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          ></th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="user in users"
          :key="user._id"
          class="hover:bg-gray-50 cursor-pointer"
        >
          <td class="px-4 py-2 border border-gray-300">{{ user.username }}</td>
          <td class="px-4 py-2 border border-gray-300">
            {{ user.email }}
          </td>
          <td class="px-4 py-2 border border-gray-300">
            {{ user.phoneNumber }}
          </td>
          <td class="px-4 py-2 border border-gray-300">
            <button class="text-red-500">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const users = ref([]);
const error = ref(null);

onMounted(async () => {
  try {
    const response = await fetch(
      'http://localhost:5000/api/v1/users',

      {
        method: 'GET',
        headers: {
          Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
        },
      }
    );

    const data = await response.json();
    users.value = data;
  } catch (err) {
    console.error('Unexpected Error:', err);
  }
});
</script>

<style scoped></style>
