<template>
  <div class="mx-10">
    <div class="w-1/2 flex justify-between items-center mb-6">
      <h2 class="text-2xl font-semibold">Admins</h2>
      <nuxt-link
        to="/admins/add"
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
          >
            Roles
          </th>

          <th
            class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
          ></th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="admin in admins"
          :key="admin._id"
          class="hover:bg-gray-50 cursor-pointer"
        >
          <td class="px-4 py-2 border border-gray-300">{{ admin.username }}</td>
          <td class="px-4 py-2 border border-gray-300">
            {{ admin.email }}
          </td>
          <td class="px-4 py-2 border border-gray-300">
            {{ admin.phoneNumber }}
          </td>
          <td class="px-4 py-2 border border-gray-300">
            {{ admin.roles.length }}
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

const admins = ref([]);
const error = ref(null);

onMounted(async () => {
  try {
    const response = await fetch(
      'http://localhost:5000/api/v1/admins',

      {
        method: 'GET',
        headers: {
          Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
        },
      }
    );

    const data = await response.json();
    console.log(data);
    admins.value = data;
  } catch (err) {
    console.error('Unexpected Error:', err);
  }
});
</script>

<style scoped></style>
