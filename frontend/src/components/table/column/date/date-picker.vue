<template>
  <v-container grid-list-md>
    <v-layout row wrap>
      <v-flex xs12 lg6>
        <v-menu v-model="menu1" :close-on-content-click="false" full-width max-width="200">
          <template v-slot:activator="{ on }">
            <v-text-field
              :value="computedDateFormattedMomentjs"
              clearable
              label="Formatted with Moment.js"
              readonly
              v-on="on"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date" @change="menu1 = false"></v-date-picker>
        </v-menu>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
// import moment from 'moment';

// export default {
//   data: () => ({
//     date: new Date().toISOString().substr(0, 10),
//     menu1: false,
//     menu2: false,
//   }),
//   computed: {
//     computedDateFormattedMomentjs() {
//       return this.date ? moment(this.date).format('dddd, MMMM Do YYYY') : '';
//     },
//   },
// };
// </script>
