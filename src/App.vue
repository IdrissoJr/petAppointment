<template>
  <div id="main-app">
    <add-appointment @add="addApt" />
    <search-appointments
      @searchRecords="seachApt"
      @request-key="changeKey"
      @request-dir="changeDir"
      :myKey="filterKey"
      :myDir="filterDir"
    />
    <appointment-list
      :appointments="filterApts"
      @remove="removeApt"
      @edit="editItem"
    />
  </div>
</template>

<script>
import AppointmentList from "@/components/AppointmentList";
import AddAppointment from "@/components/AddAppointment";
import SearchAppointments from "@/components/SearchAppointments";
import _ from "lodash";
import axios from "axios";

export default {
  name: "MainApp",
  data() {
    return {
      appointments: [],
      searchTerms: "",
      filterKey: "petName",
      filterDir: "asc",
      aptIndex: 0,
    };
  }, //data
  components: { AppointmentList, AddAppointment, SearchAppointments },
  computed: {
    searchedApts() {
      return this.appointments.filter((item) => {
        return (
          item.petName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.petOwner.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.aptNotes.toLowerCase().match(this.searchTerms.toLowerCase())
        );
      });
    },

    filterApts() {
      return _.orderBy(
        this.searchedApts,
        (item) => {
          return item[this.filterKey].toLowerCase();
        },
        this.filterDir
      );
    },
  },
  methods: {
    addApt(apt) {
      apt.aptId = this.aptIndex++;
      this.appointments.push(apt);
    },
    seachApt(terms) {
      this.searchTerms = terms;
    },
    changeKey(k) {
      this.filterKey = k;
    },
    changeDir(d) {
      this.filterDir = d;
    },
    removeApt(apt) {
      // for (let i = 0; i < this.appointments.length; i++) {
      //   if (apt == this.appointments[i]) {
      //     this.appointments.splice(i, 1);
      //   }
      // }
      this.appointments = _.without(this.appointments, apt);
    },
    editItem(id, field, text) {
      const aptIndex = _.findIndex(this.appointments, {
        aptId: id,
      });
      this.appointments[aptIndex][field] = text;
    },
  },
  mounted() {
    axios.get("./data/appointments.json").then(
      (response) =>
        (this.appointments = response.data.map((item) => {
          item.aptId = this.aptIndex++;
          return item;
        }))
    );
  },
};
</script>

<style lang="scss">
#main-app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
