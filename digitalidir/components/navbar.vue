<template>
  <div
    class="border-b border-b-gray-100 w-full mb-4 flex justify-between items-center py-4 px-3 pr-6 text-blue-900"
  >
    <div class="sm:hidden">
      <FontAwesomeIcon
        icon="bars"
        class="text-gray-600 w-6 h-6 text-2xl cursor-pointer"
      />
    </div>
    <h1 class="text-2xl font-medium max-md:hidden">Welcome Our Admin</h1>
    <nuxt-link to="/login">
      <FontAwesomeIcon
        icon="user"
        class="text-blue-900 w-6 h-10 cursor-pointer text-2xl"
      />
    </nuxt-link>
  </div>
</template>

<script setup></script>

<style scoped></style>
