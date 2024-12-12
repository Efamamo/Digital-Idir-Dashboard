<template>
  <div class="max-w-xl mx-auto shadow-md rounded-md p-10 mt-8 md:mt-40">
    <h3 class="text-center text-2xl font-bold">Add Admin</h3>
    <form v-on:submit.prevent="handleSubmit">
      <div class="flex flex-col gap-2 mb-4">
        <label for="username">Username</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="text"
          id="username"
          v-model="username"
        />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="email">Email</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="email"
          id="email"
          v-model="email"
        />
      </div>
      <div class="flex flex-col gap-2 mb-4">
        <label for="phone">Phone Number</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="tel"
          id="phone"
          v-model="phoneNumber"
        />
      </div>
      <div class="flex flex-col gap-2 mb-4">
        <label for="password">Password</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="password"
          id="password"
          v-model="password"
        />
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
        <div class="flex gap-1 w-56" v-for="role in roles" :key="role._id">
          <input
            type="checkbox"
            :id="`role-${role._id}`"
            v-model="selectedRoles"
            :value="role._id"
          />
          <label :for="`role-${role._id}`">
            {{ role.role_name }}
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
const username = ref('');
const email = ref('');
const password = ref('');
const phoneNumber = ref('');
const roles = ref([]);
const error = ref('');
const selectedRoles = ref([]);
const selectAll = ref(false);

useHead({
  title: 'DigitalIdir | Add Admin',
});

onMounted(async () => {
  try {
    const response = await fetch('http://localhost:5000/api/v1/roles', {
      headers: {
        Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
      },
    });

    const data = await response.json();

    if (response.ok) {
      roles.value = data;
    } else {
      error.value = data;
    }
  } catch (e) {
    error.value = e;
  }
});

const toggleSelectAll = () => {
  if (selectAll.value) {
    selectedRoles.value = roles.value.map((role) => role._id);
  } else {
    selectedRoles.value = [];
  }
};

const handleSubmit = async () => {
  try {
    const response = await fetch(`http://localhost:5000/api/v1/admins`, {
      method: 'POST',
      body: JSON.stringify({
        username: username.value,
        email: email.value,
        phoneNumber: phoneNumber.value,
        password: password.value,
        roles: roles.value,
      }),
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
      },
    });

    const data = await response.json();

    if (response.ok) {
      window.location.href = '/admins';
    } else {
      console.log(data);
    }
  } catch (e) {
    console.error(e);
  }
};
</script>

<style scoped></style>
