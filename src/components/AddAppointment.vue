<template>
  <div class="mx-6 md:mx-24 flex justify-center md:justify-start mb-6">
    <div class="w-5/6 md:w-full border-2">
      <h4
        class="text-white bg-green-500 font-bold text-center p-4 cursor-pointer"
        @click="addToggle = !addToggle"
      >
        <font-awesome-icon icon="plus" class="mr-3" /> Add Appointment
      </h4>

      <form
        class="px-4"
        :class="{ hidden: addToggle }"
        @submit.prevent="requestAdd"
      >
        <label class="block font-bold mt-4 mb-1 text-gray-700" for="pet-name"
          >Pet Name</label
        >
        <div>
          <input
            class="w-full p-2 border-2 border-gray-200 focus:outline-none focus:border-gray-400 rounded"
            type="text"
            id="pet-name"
            placeholder="Pet's Name"
            v-model="formData.petName"
            required
          />
        </div>

        <label class="block font-bold mt-4 mb-1 text-gray-700" for="owner-name"
          >Pet Owner</label
        >
        <div>
          <input
            class="w-full p-2 border-2 border-gray-200 focus:outline-none focus:border-gray-400 rounded"
            type="text"
            id="owner-name"
            placeholder="Owner's Name"
            v-model="formData.petOwner"
            required
          />
        </div>

        <label class="block font-bold mt-4 mb-1 text-gray-700" for="apt-date"
          >Date</label
        >
        <div>
          <input
            class="w-full p-2 border-2 border-gray-200 focus:outline-none focus:border-gray-400 rounded"
            type="date"
            id="apt-date"
            v-model="formData.aptDate"
            required
          />
        </div>

        <label class="block font-bold mt-4 mb-1 text-gray-700" for="apt-time"
          >Time</label
        >
        <div>
          <input
            class="w-full p-2 border-2 border-gray-200 focus:outline-none focus:border-gray-400 rounded"
            type="time"
            id="apt-time"
            v-model="formData.aptTime"
            required
          />
        </div>

        <label class="block font-bold mt-4 mb-1 text-gray-700" for="apt-notes"
          >Apt. Notes</label
        >
        <div>
          <textarea
            class="w-full p-2 border-2 border-gray-200 focus:outline-none focus:border-gray-400 rounded"
            name="apt-notes"
            id="apt-notes"
            cols="50"
            rows="4"
            placeholder="Appointment Notes"
            v-model="formData.aptNotes"
            required
          ></textarea>
        </div>

        <div class="mt-3 mb-4 text-center">
          <button
            class="bg-green-500 text-white font-bold p-2 rounded focus:outline-none focus:bg-green-600"
            type="submit"
          >
            Add Appointment
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddAppointment",
  data() {
    return {
      formData: [],
      addToggle: true,
    };
  }, //data
  methods: {
    requestAdd() {
      this.formData = {
        petName: this.formData.petName,
        petOwner: this.formData.petOwner,
        aptDate: this.formData.aptDate + " " + this.formData.aptTime,
        aptNotes: this.formData.aptNotes,
      };
      this.$emit("add", this.formData);
      this.formData = [];
      this.addToggle = true;
    },
  },
};
</script>
