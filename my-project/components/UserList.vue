<!-- components/UserList.vue -->
<template>
  <div>
    <div class="px-2 sm:px-5 mb-4">
      <div
        class="bg-white rounded-lg border border-gray-100 shadow-[0_2px_8px_rgba(0,0,0,0.08)] p-4 sm:p-5"
      >
        <div
          class="flex flex-col sm:flex-row gap-3 sm:gap-4 items-stretch sm:items-center justify-between"
        >
          <!-- Search Input -->
          <div class="relative flex-grow">
            <input
              type="text"
              placeholder="Search users..."
              v-model="search"
              class="w-full border border-gray-200 px-4 py-2 pl-4 pr-10 rounded-lg text-sm sm:text-base transition-all duration-200 shadow-sm"
            />
          </div>

          <!-- Sort and Pagination -->
          <div
            class="flex flex-col sm:flex-row items-stretch sm:items-center gap-3 sm:gap-4 w-full sm:w-auto"
          >
            <!-- Sort Dropdown -->
            <div class="relative">
              <select
                v-model="sortBy"
                class="border border-gray-200 py-2 rounded-lg text-sm w-full transition-all duration-200 shadow-sm cursor-pointer"
              >
                <option value="name">Sort by Name</option>
                <option value="date">Sort by Date</option>
                <option value="country">Sort by Country</option>
              </select>
            </div>

            <!-- Pagination -->
            <div
              class="flex items-center gap-2 bg-gray-50 px-3 py-1 rounded-lg border border-gray-100 shadow-sm"
            >
              <button
                @click="prevPage"
                :disabled="currentPage === 1"
                class="p-1 rounded-md hover:bg-gray-100 disabled:opacity-50 disabled:hover:bg-transparent transition-colors duration-200 text-gray-600 cursor-pointer"
              >
                &lt;
              </button>
              <span
                class="text-xs sm:text-sm font-medium text-gray-600 whitespace-nowrap"
              >
                Page {{ currentPage }} of {{ totalPages }}
              </span>
              <button
                @click="nextPage"
                :disabled="currentPage === totalPages"
                class="p-1 rounded-md hover:bg-gray-100 disabled:opacity-50 disabled:hover:bg-transparent transition-colors duration-200 text-gray-600 cursor-pointer"
              >
                &gt;
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="px-2 sm:px-5 grid grid-cols-1 gap-2 sm:gap-4">
      <div class="hidden sm:flex px-5 sm:px-10 text-gray-400 text-sm">
        <div class="w-1/6">Date</div>
        <div class="w-1/3">Name</div>
        <div class="w-1/8">Gender</div>
        <div class="w-1/5">Country</div>
        <div class="w-1/5 flex justify-end">Email</div>
      </div>

      <div
        v-for="user in paginatedUsers"
        :key="user.login.uuid"
        @click="$emit('user-selected', user)"
        class="px-4 sm:px-6 py-3 bg-white rounded-lg border border-gray-100 shadow-[0_2px_8px_rgba(0,0,0,0.08)] hover:border-sky-400 hover:shadow-[0_2px_8px_rgba(56,182,255,0.2)] transition-all duration-200 cursor-pointer group"
      >
        <div
          class="py-2 sm:py-4 px-2 sm:px-5 flex flex-col sm:flex-row items-start sm:items-center gap-2 sm:gap-0"
        >
          <div class="sm:hidden w-full flex flex-col gap-1">
            <div class="font-semibold text-base group-hover:text-sky-400">
              {{ user.name.first }} {{ user.name.last }}
            </div>
            <div class="flex justify-between text-xs text-gray-500">
              <span class="capitalize">{{ user.gender }}</span>
              <span>{{ user.location.country }}</span>
            </div>
          </div>

          <div class="hidden sm:flex w-1/6 text-gray-400 text-sm">
            {{
              new Date(user.registered.date).toLocaleDateString("en-GB", {
                day: "numeric",
                month: "short",
                year: "numeric",
              })
            }}
          </div>

          <div
            class="hidden sm:flex w-1/3 font-semibold text-sm group-hover:text-sky-400"
          >
            {{ user.name.first }} {{ user.name.last }}
          </div>

          <div class="hidden sm:flex w-1/8 text-gray-400 text-sm capitalize">
            {{ user.gender }}
          </div>

          <div class="hidden sm:flex w-1/5 text-sm">
            {{ user.location.country }}
          </div>

          <div
            class="hidden sm:flex w-1/5 justify-end text-gray-500 text-xs sm:text-sm"
          >
            {{ user.email }}
          </div>

          <div class="sm:hidden w-full text-xs text-gray-500 truncate">
            {{ user.email }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";

const props = defineProps({
  users: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["user-selected"]);

const search = ref("");
const sortBy = ref("name");
const currentPage = ref(1);
const itemsPerPage = 5;

const filteredUsers = computed(() => {
  let filtered = props.users.filter((user) =>
    `${user.name.first} ${user.name.last} ${user.email}`
      .toLowerCase()
      .includes(search.value.toLowerCase())
  );

  // Sorting logic
  if (sortBy.value === "name") {
    filtered.sort((a, b) =>
      `${a.name.first} ${a.name.last}`.localeCompare(
        `${b.name.first} ${b.name.last}`
      )
    );
  } else if (sortBy.value === "date") {
    filtered.sort(
      (a, b) => new Date(b.registered.date) - new Date(a.registered.date)
    );
  } else if (sortBy.value === "country") {
    filtered.sort((a, b) =>
      a.location.country.localeCompare(b.location.country)
    );
  }

  return filtered;
});

const totalPages = computed(() => {
  return Math.ceil(filteredUsers.value.length / itemsPerPage);
});

const paginatedUsers = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  const end = start + itemsPerPage;
  return filteredUsers.value.slice(start, end);
});

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
};

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
};

watch([search, sortBy], () => {
  currentPage.value = 1;
});
</script>
