<template>
  <div class="container mx-auto">
    <h2 class="text-2xl font-semibold">Permissions</h2>
    <div class="flex gap-20 m-10">
      <table
        class="w-1/2 mx-auto border-collapse border border-gray-200 bg-white shadow-md rounded-md mb-6"
      >
        <thead class="bg-gray-100">
          <tr>
            <th
              class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
            >
              Code Name
            </th>
            <th
              class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
            >
              Description
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="permission in permissions.slice(0, 18)"
            :key="permission._id"
            class="hover:bg-gray-50 cursor-pointer"
          >
            <td class="px-4 py-2 border border-gray-300">
              {{ permission.code_name }}
            </td>
            <td class="px-4 py-2 border border-gray-300">
              {{ permission.description }}
            </td>
          </tr>
        </tbody>
      </table>

      <!-- Second Table -->
      <table
        class="w-1/2 mx-auto border-collapse border border-gray-200 bg-white shadow-md rounded-md"
      >
        <thead class="bg-gray-100">
          <tr>
            <th
              class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
            >
              Code Name
            </th>
            <th
              class="px-4 py-2 text-left text-gray-700 font-semibold border border-gray-300"
            >
              Description
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="permission in permissions.slice(18)"
            :key="permission._id"
            class="hover:bg-gray-50 cursor-pointer"
          >
            <td class="px-4 py-2 border border-gray-300">
              {{ permission.code_name }}
            </td>
            <td class="px-4 py-2 border border-gray-300">
              {{ permission.description }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const permissions = ref([]);
const error = ref(null);

onMounted(async () => {
  try {
    console.log(localStorage.getItem('accessToken'));
    const response = await fetch(
      'http://localhost:5000/api/v1/permissions',

      {
        method: 'GET',
        headers: {
          Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
        },
      }
    );

    const data = await response.json();
    permissions.value = data;
  } catch (err) {
    console.error('Unexpected Error:', err);
  }
});
</script>

<style scoped></style>
