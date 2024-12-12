<template>
  <div class="max-w-xl mx-auto shadow-md rounded-md p-10 mt-8 md:mt-40">
    <h3 class="text-center text-2xl font-bold">Login</h3>
    <form v-on:submit.prevent="handleSubmit">
      <div class="flex flex-col gap-2 mb-4">
        <label for="email">Email</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="email"
          id="email"
          v-model="email"
        />
        <p v-if="emailError">{{ emailError }}</p>
      </div>
      <div class="flex flex-col gap-2 mb-4">
        <label for="password">Password</label>
        <input
          class="border border-gray-300 focus:outline-none p-1 rounded-sm"
          type="password"
          id="password"
          v-model="password"
        />
        <p v-if="passwordError">{{ passwordError }}</p>
      </div>

      <button
        type="submit"
        class="w-full bg-blue-500 p-1.5 mt-4 text-white font-semibold rounded-sm"
      >
        Login
      </button>
    </form>
  </div>
</template>

<script setup>
useHead({
  title: 'DigitalIdir | Login',
});

const email = ref('');
const password = ref('');

const emailError = '';
const passwordError = '';

const handleSubmit = async () => {
  try {
    const { data, error } = await useFetch(
      'http://localhost:5000/api/v1/auth/login',
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          email: email.value,
          password: password.value,
        }),
      }
    );

    if (error.value) {
      console.error('Error:', error.value);
      return;
    }

    localStorage.setItem('accessToken', data.value.accessToken);
    localStorage.setItem('refreshToken', data.value.refreshToken);

    window.location.href = '/dashboard';

    // Handle successful login, e.g., store token or redirect
  } catch (err) {
    console.error('Unexpected Error:', err);
  }
};

definePageMeta({
  layout: 'login',
});
</script>

<style scoped></style>
