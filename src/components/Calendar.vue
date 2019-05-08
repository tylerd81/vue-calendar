<template>
  <div class="calendar">
    <h1>{{getMonthData(month).month}} {{year}}</h1>
    <table class="calendar">
      <thead>
        <tr>
          <td>Sun</td>
          <td>Mon</td>
          <td>Tue</td>
          <td>Wed</td>
          <td>Thr</td>
          <td>Fri</td>
          <td>Sat</td>
        </tr>
      </thead>

      <tr v-for="week in 6">
        <td class="day" v-for="day in 7">
          <!-- <div>{{getNextDate()}}</div> Create a Day component -->
          <day :class="{currentDay: isCurrentDay()}" :date="getNextDate()"></day>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import Day from './Day.vue';
let nextDate = 0;

export default {
  components: {
    day: Day,
  },
  props: {
    year : {
      type: Number,
      required: true,
    },
    month : {
      type: Number,
      required: true,
    }
  },
  data() {
    return {
      dateTime: null,
      calendarArray: [],
      currentDay: -1,
    };
  },
  watch : {
    month: function() {
      this.init();
    }
  },
  methods: {
    getMonthData(month) {
      switch(month) {
        case 1: return {month: "January", numDays: 31};
        case 2: return {month: "February", numDays: 28 + this.isLeapYear()};
        case 3: return {month: "March", numDays: 31};
        case 4: return {month: "April", numDays: 30};
        case 5: return {month: "May", numDays: 31};
        case 6: return {month: "June", numDays: 30};
        case 7: return {month: "July", numDays: 31};
        case 8: return {month: "August", numDays: 31};
        case 9: return {month: "September", numDays: 30};
        case 10: return {month: "October", numDays: 31};
        case 11: return {month: "November", numDays: 30};
        case 12: return {month: "December", numDays: 31};
      }
    },
    isCurrentDay() {
      if(this.calendarArray[nextDate] === this.currentDay) {
        return true;
      }else{
        return false;
      }
    },
    isLeapYear() {
      if(this.year % 4 === 0) {
        if(this.year % 100 !== 0 && this.year % 400 !== 0) {
          return 1;
        }
      }
      return 0;
    },
    init() {
      nextDate = 0;
      this.dateTime = new Date(this.year, this.month - 1, 1);
      this.calendarArray = [];
      this.currentDay = -1;
      // get the starting day
      let startingDay = this.dateTime.getDay();
      let currentDate = 1;
      let numDays = this.getMonthData(this.month).numDays;

      // start the array the the correct starting day
      let currentDay = 0;
      while(currentDay < startingDay) {
        this.calendarArray.push(0);
        currentDay++;
      }

      for(let d = 0; d < numDays; d++) {
        this.calendarArray.push(currentDate++);
      }

      while(this.calendarArray.length < 42) {
        this.calendarArray.push(0);
      }
    
      let now = new Date();
      if(this.dateTime.getMonth() === now.getMonth() && this.dateTime.getYear() === now.getYear()) {
        this.currentDay = now.getDate();
      }
    },
    getNextDate() {
      return this.calendarArray[nextDate++];
    }
  },
  created() {
    console.log("Created Called");
    this.init();
  }
}
</script>

<style>
table.calendar {
  width: 90vw;
  /* border: solid 1px #000; */
  border-collapse: collapse;
}
thead tr td {
  text-align: center;
  background-color: lightgray;
}

td {
  padding: 0;
  border: solid 1px #000;
}

td.day {
  height: 5rem;
  width: 3rem;
  text-align: top;
  margin: 0;
}
td div.no-day {
  background-color: lightgray;
  border: none;
}
td.day div {
  height: 100%;
  width: 100%;
}

.currentDay {
  background-color: lightgreen;
}
</style>
