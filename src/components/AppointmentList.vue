<template>
  <div class="mt-3 mx-6 md:mx-24 flex justify-center md:justify-start">
    <div class="w-5/6 md:w-full">
      <div
        class="mb-3 pb-3 border-b-2 flex justify-between"
        v-for="item in appointments"
        :key="item.aptIndex"
      >
        <div class="flex items-start">
          <button
            class="mr-2 px-2 py-1 rounded bg-red-600 text-white focus:outline-none"
            @click="$emit('remove', item)"
          >
            <font-awesome-icon icon="trash" size="sm" />
          </button>

          <div>
            <h3
              class="text-green-500 font-bold text-2xl mb-1"
              contenteditable="contenteditable"
              @blur="
                $emit('edit', item.aptId, 'petName', $event.target.innerText)
              "
            >
              {{ item.petName }}
            </h3>
            <h4 class="font-bold text-base">
              <span class="text-green-500">Owner: </span
              ><span
                contenteditable="contenteditable"
                @blur="
                  $emit('edit', item.aptId, 'petOwner', $event.target.innerText)
                "
                >{{ item.petOwner }}</span
              >
            </h4>
            <p
              class="font-medium"
              contenteditable="contenteditable"
              @blur="
                $emit('edit', item.aptId, 'aptNotes', $event.target.innerText)
              "
            >
              {{ item.aptNotes }}
            </p>
          </div>
        </div>

        <p class="font-medium text-xs md:text-base">
          {{ formattedDate(item.aptDate) }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "AppointmentList",
  props: ["appointments"],
  methods: {
    formattedDate(date) {
      return moment(new Date(date)).format("MM-DD-YY, h:mm a");
    },
  },
};
</script>
