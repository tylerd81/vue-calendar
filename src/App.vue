<template>
  <div id="app">
    <button @click="prevMonth">Prev</button>
    <button @click="nextMonth">Next</button>
    <calendar :year="year" :month="month"></calendar>
  </div>
</template>

<script>
  import Calendar from './components/Calendar.vue';

  export default {
    components : {
      calendar: Calendar,
    },
    data() {
      return {
        month: 5,
        year: 2019,
      };
    },
    methods: {
      nextMonth() {
        if(this.month < 12) {
          this.month++;
        }else{
          this.month = 1;
          this.year++;
        }
      },
      prevMonth() {
        if(this.month === 1) {
          this.month = 12;
          this.year--;
        }else{
          this.month--;
        }
      }
    }
  }
</script>

<style>
body {
  font-family: "Open Sans";
}
</style>
