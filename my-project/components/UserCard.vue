<template>
  <div class="relative">
    <div
      class="absolute top-0 left-0 w-full h-[calc(10rem+195px)] sm:h-[calc(5rem+65px)] bg-sky-400 z-0"
    ></div>

    <div
      class="relative z-1 py-4 px-4 sm:py-6 sm:px-6 flex flex-col sm:flex-row items-start sm:items-center"
    >
      <div class="flex justify-center w-full sm:w-auto mb-4 sm:mb-0">
        <img
          :src="user.image"
          class="w-40 h-40 rounded-lg sm:mr-6 border-white relative z-1"
          alt="User Image"
        />
      </div>

      <div
        class="flex flex-col sm:flex-row items-center sm:items-start justify-between w-full gap-4"
      >
        <div
          class="flex flex-col sm:flex-row sm:items-center gap-2 sm:gap-4 text-center sm:text-left"
        >
          <div>
            <h1
              class="text-2xl sm:text-3xl md:text-4xl font-bold text-white break-words"
            >
              {{ user.name }}
            </h1>
            <p class="text-white text-sm sm:text-base">
              Last online: {{ user.lastOnline }}
            </p>
          </div>

          <div class="flex flex-col sm:flex-row gap-2 w-full sm:w-auto">
            <button
              class="bg-white text-sky-500 px-3 py-1 sm:px-4 sm:py-2 rounded flex items-center justify-center gap-1 text-xs sm:text-sm font-medium"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="size-6"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M6 12 3.269 3.125A59.769 59.769 0 0 1 21.485 12 59.768 59.768 0 0 1 3.27 20.875L5.999 12Zm0 0h7.5"
                />
              </svg>

              Send Message
            </button>
            <button
              class="border border-white text-white px-3 py-1 sm:px-4 sm:py-2 rounded text-xs sm:text-sm font-medium flex items-center justify-center gap-1"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="size-6"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M12 4.5v15m7.5-7.5h-15"
                />
              </svg>

              Add Friend
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  user: {
    type: Object,
    required: true,
  },
});
</script>

<style scoped>
button {
  min-width: fit-content;
}

@media (max-width: 640px) {
  .border-4 {
    border-width: 3px;
  }
}
</style>
