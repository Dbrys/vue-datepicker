<template>
  <div class="datePickerContainer">
    <input type="text" v-on:click="getMonthDays" placeholder="mm/dd/yyyy" />
    <div id="overlay" v-bind:style="{display:overlayView}"></div>
    <div v-if="!isHidden" class="calContainer">
      <div class="calendarMonth">
        <button id="prevBtn" @click="prevBtnClick">{{prevBtn}}</button>
        <div id="date">
          <span class="month-val">{{curMonth}}</span>
          <span class="year-val">{{currentYear}}</span>
        </div>
        <button id="nextBtn" v-on:click="nextBtnClick">{{nextBtn}}</button>
      </div>
      <div class="calendar">
        <mainContainer :currDay="this.days" :listOfDays="this.daysAry" @setDays="setDays" />
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data: function() {
    return {
      isHidden: true,
      overlayView: "none",
      curMonth: "",
      days: null,
      prevBtn: `<`,
      nextBtn: `>`,
      months: {
        January: 0,
        February: 1,
        March: 2,
        April: 3,
        May: 4,
        June: 5,
        July: 6,
        August: 7,
        September: 8,
        October: 9,
        November: 10,
        December: 11
      },
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      daysAry: []
    };
  },

  components: {
    mainContainer
  },

  name: "datePicker",

  methods: {
    getMonthDays: function() {
      this.isHidden = !this.isHidden;
      this.overlayView === "none"
        ? (this.overlayView = "block")
        : (this.overlayView = "none");
      console.log(this.overlayView);
      const month = new Date().getMonth();
      this.curMonth = this.getKeyValue(this.months, month);
      if (this.curMonth != null) {
        this.days = new Date(this.currentYear, this.currentMonth, 0).getDate();
      }
    },

    getKeyValue: function(obj, val) {
      for (let item in obj) {
        if (obj.hasOwnProperty(item)) {
          if (obj[item] === val) {
            return item;
          }
        }
      }
    },

    nextBtnClick: function(e) {
      e.preventDefault();
      this.currentMonth++;
      if (this.currentMonth > 11) {
        this.currentMonth = 0;
        this.currentYear++;
      }
      this.setMonth(this.currentMonth);
      this.setDays();
      // console.log(this.days);
    },

    prevBtnClick: function(e) {
      e.preventDefault();
      this.currentMonth--;
      if (this.currentMonth < 0) {
        this.currentMonth = 11;
        this.currentYear--;
      }

      this.setMonth(this.currentMonth);
      this.setDays();
    },

    setDays: function() {
      this.setMonth(this.currentMonth);
      if (this.daysAry != undefined) {
        this.daysAry = [];
        for (let i = 1; i <= this.days; i++) {
          this.daysAry.push(i);
        }
      }
    },

    setMonth: function(curMonth) {
      this.curMonth = this.getKeyValue(this.months, curMonth);
      this.days = new Date(this.currentYear, curMonth + 1, 0).getDate();
    }
  }
};

import mainContainer from "./DatepickerMainContainer";
</script>


<style>
.datePickerContainer {
  margin: auto;
  width: 25%;
}

.calContainer {
  border-width: 2px;
  border-style: solid;
  border-color: black;
}

.calendarMonth {
  height: 75px;
  display: flex;
  flex-direction: row;
}

#date {
  display: flex;
  justify-content: center;
  width: 100%;
  height: 100%;
}

/* #overlay{
position: fixed; 
  display: none; 
  width: 100%; 
  height: 100%; 
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color:transparent;
  z-index: 2; 
  cursor: pointer; 
} */

.month-val,
.year-val {
  font-style: italic;
  font-weight: bold;
  font-size: 1em;
}

.year-val {
  padding-left: 15px;
}

#prevBtn {
  flex-basis: 1;
  height: 50%;
}

#nextBtn {
  flex-basis: 1;
  height: 50%;
}

.calendar {
  display: block;
}
</style>
