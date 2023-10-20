<template>
  <v-container class="ma-5">
    <v-row justify="center">
      <v-col cols="12" sm="8" md="6">
        <v-card>
          <v-card-title class="headline">
            Restaurant Reservation
          </v-card-title>
          <v-card-text>
            <v-form @submit="submitReservation">
              <v-text-field v-model="name" label="ชื่อคนจอง" required></v-text-field>
              <v-date-picker v-model="date" label="Reservation Date" required></v-date-picker>
              <v-time-picker v-model="time" label="Reservation Time" required></v-time-picker>
              <v-text-field v-model="partySize" label="จำนวนคน" type="number" required></v-text-field>
              <v-textarea v-model="specialRequests" label="คำขอพิเศษ"></v-textarea>
              <v-btn color="primary" type="submit">Submit</v-btn>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      date: new Date(),
      time: new Date(),
      partySize: 1,
      specialRequests: "",
    };
  },
  methods: {
    submitReservation() {
      // Add your reservation submission logic here
      console.log("Reservation submitted!");
    },
  },
};
</script>

<style>

</style>
