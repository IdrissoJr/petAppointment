<template>
  <div class="mx-6 md:mx-24 flex justify-center md:justify-start mb-6">
    <div class="w-5/6 md:w-full">
      <input
        type="text"
        v-model="searchTerm"
        placeholder="Search Appointments"
        class="w-1/2 sm:w-2/3 md:w-4/5 py-2 px-3 text-sm rounded-l-lg border-2 border-gray-200 focus:outline-none focus:border-gray-300"
      />

      <div class="w-1/2 sm:w-1/3 md:w-1/5 relative inline-block">
        <div>
          <button
            type="button"
            class="inline-flex text-sm justify-center px-4 py-2 w-full rounded-r-lg border border-gray-300 shadow-sm bg-white font-medium text-gray-700 hover:bg-gray-50 focus:outline-none"
            id="options-menu"
            aria-haspopup="true"
            aria-expanded="true"
            @click="toggleMenu = !toggleMenu"
          >
            Sort by
            <svg
              class="-mr-1 ml-2 h-5 w-5"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="currentColor"
              aria-hidden="true"
            >
              <path
                fill-rule="evenodd"
                d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                clip-rule="evenodd"
              />
            </svg>
          </button>
        </div>

        <div
          class="origin-top-right absolute right-0 mt-2 w-40 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 divide-y divide-gray-100"
          role="menu"
          aria-orientation="vertical"
          aria-labelledby="options-menu"
          v-show="toggleMenu"
        >
          <div class="py-1">
            <a
              href="#"
              class="flex justify-between items-center px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 hover:text-gray-900"
              role="menuitem"
              @click.prevent="$emit('request-key', 'petName')"
              >Pet Name
              <font-awesome-icon
                v-if="myKey === 'petName'"
                icon="check"
                class="text-xs"
            /></a>
            <a
              href="#"
              class="flex justify-between items-center px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 hover:text-gray-900"
              role="menuitem"
              @click.prevent="$emit('request-key', 'aptDate')"
              >Date
              <font-awesome-icon
                v-if="myKey === 'aptDate'"
                icon="check"
                class="text-xs"
            /></a>
            <a
              href="#"
              class="flex justify-between items-center px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 hover:text-gray-900"
              role="menuitem"
              @click.prevent="$emit('request-key', 'petOwner')"
              >Owner
              <font-awesome-icon
                v-if="myKey === 'petOwner'"
                icon="check"
                class="text-xs"
            /></a>
          </div>
          <div class="py-1">
            <a
              href="#"
              class="flex justify-between items-center px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 hover:text-gray-900"
              role="menuitem"
              @click.prevent="$emit('request-dir', 'asc')"
              >Asc
              <font-awesome-icon
                v-if="myDir === 'asc'"
                icon="check"
                class="text-xs"
            /></a>
            <a
              href="#"
              class="flex justify-between items-center px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 hover:text-gray-900"
              role="menuitem"
              @click.prevent="$emit('request-dir', 'desc')"
              >Desc
              <font-awesome-icon
                v-if="myDir === 'desc'"
                icon="check"
                class="text-xs"
            /></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchAppointments",
  data() {
    return {
      searchTerm: "",
      toggleMenu: false,
    };
  }, //data
  props: ["myKey", "myDir"],
  watch: {
    searchTerm() {
      this.$emit("searchRecords", this.searchTerm);
    },
  },
};
</script>
