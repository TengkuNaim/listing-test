<!-- components/UserDialog.vue -->
<template>
    <div
      v-if="user"
      class="z-2 fixed inset-0 bg-black bg-opacity-30 flex items-center justify-center p-4"
    >
      <div
        class="bg-white p-4 sm:p-6 rounded-lg shadow-lg max-w-md w-full relative max-h-[90vh] overflow-y-auto"
      >
        <button
          class="absolute top-2 right-2 text-gray-500 text-2xl p-2 cursor-pointer"
          @click="$emit('close')"
        >
          &times;
        </button>
        <div class="text-center space-y-3">
          <img
            :src="user.picture.large"
            alt="avatar"
            class="mx-auto rounded-full mb-4 w-20 h-20 sm:w-24 sm:h-24"
          />
          <h2 class="text-lg sm:text-xl font-bold">
            {{ user.name.title }} {{ user.name.first }}
            {{ user.name.last }}
          </h2>
          <p class="text-sm sm:text-base text-gray-600">
            Status: Inactive
          </p>
          <p class="text-sm sm:text-base text-gray-600 capitalize">
            Gender: {{ user.gender }}
          </p>
          <p class="text-sm sm:text-base text-gray-600">
            Country: {{ user.location.country }}
          </p>
          <p class="text-sm sm:text-base text-gray-600">
            Email: {{ user.email }}
          </p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps({
    user: {
      type: Object,
      default: null,
    },
  });
  
  defineEmits(["close"]);
  </script>