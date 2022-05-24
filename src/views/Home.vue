<template>
  <div class="bg-gray-700 w-full h-screen p-5 flex flex-col select-none">
    <h1 class="text-center text-7xl text-white font-bold">Augustin timing</h1>
    <p class="text-center text-white mt-10">{{ now }}</p>
    <div class="flex flex-row flex-wrap py-20">
      <div v-for="(data, iterator) in compareDataDates" v-bind:key="iterator" class="max-w-7xl mx-auto sm:px-6 lg:px-8 bg-gray-200 transition duration-300 hover:bg-white rounded-lg p-5">
        <p class="text-center font-bold text-lg text-green-500">{{ data.title }}</p>
        <p class="font-medium text-6xl text-center mt-3">J - {{ compareDate(data.endDate, now) }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import {DateTime} from "luxon";

export default {
  name: "Home",
  data() {
    return{
      now: DateTime.now().toFormat("dd-MM-yyyy HH:mm:ss"),
      compareDataDates: [
        {
          title: "Mariage Zoé et Augustin",
          endDate: "05-08-2023 08:00:00"
        },
        {
          title: "Fin des études d'Augustin",
          endDate: "22-09-2023 23:59:00"
        },
      ]
    }
  },
  methods:{
    compareDate(first_date, now){
      return Math.round(DateTime.fromFormat(first_date,"dd-MM-yyyy HH:mm:ss").diff(DateTime.fromFormat(now, "dd-MM-yyyy HH:mm:ss"), ['days']).toObject().days);
    }
  },
  mounted() {
    setInterval(() => {
      this.now = DateTime.now().toFormat("dd-MM-yyyy HH:mm:ss");
    }, 1000);
  }
};
</script>
