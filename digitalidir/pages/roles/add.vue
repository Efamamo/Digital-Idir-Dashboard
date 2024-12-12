<template>
  <div class="max-w-4xl mx-auto shadow-md rounded-md p-10 mt-8">
    <h3 class="text-center text-2xl font-bold">Add Role</h3>
    <form v-on:submit.prevent="handleSubmit">
      <div class="flex flex-col gap-2 mb-4">
        <label for="title">Name</label>
        <input
          v-model="roleName"
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="text"
          id="title"
        />
      </div>
      <div class="flex flex-col gap-2 mb-4">
        <label for="description">Description</label>
        <textarea
          v-model="description"
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          id="description"
        ></textarea>
      </div>
      <div class="flex gap-1 w-56 mt-6">
        <input
          type="checkbox"
          id="select_all"
          v-model="selectAll"
          @change="toggleSelectAll"
        />
        <label for="select_all"> Select All </label>
      </div>
      <div class="flex flex-wrap gap-4 justify-between my-6 pl-4">
        <div
          class="flex gap-1 w-56"
          v-for="permission in permissions"
          :key="permission._id"
        >
          <input
            type="checkbox"
            :id="`permission-${permission._id}`"
            v-model="selectedPermissions"
            :value="permission._id"
          />
          <label :for="`permission-${permission._id}`">
            {{ permission.description }}
          </label>
        </div>
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
import { ref, onMounted } from 'vue';

const permissions = ref([]);
const selectedPermissions = ref([]);
const selectAll = ref(false);
const roleName = ref('');
const description = ref('');

onMounted(async () => {
  try {
    const response = await fetch('http://localhost:5000/api/v1/permissions', {
      method: 'GET',
      headers: {
        Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
      },
    });

    const data = await response.json();
    permissions.value = data;
  } catch (err) {
    console.error('Unexpected Error:', err);
  }
});

const toggleSelectAll = () => {
  if (selectAll.value) {
    selectedPermissions.value = permissions.value.map(
      (permission) => permission._id
    );
  } else {
    selectedPermissions.value = [];
  }
};

const handleSubmit = async () => {
  try {
    const response = await fetch('http://localhost:5000/api/v1/roles', {
      method: 'POST',
      body: JSON.stringify({
        role_name: roleName.value,
        permissions: selectedPermissions.value,
        description: description.value,
      }),
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
      },
    });

    if (response.ok) {
      window.location.href = '/roles';
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
