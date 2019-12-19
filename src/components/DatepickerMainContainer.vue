<template>
  <div>
    <div id="days-in-month">
      <div
        class="pointer"
        id="day"
        v-for="day in this.listOfDays"
        v-bind:key="day"
        @click="selectDay(day)"
      >{{day}}</div>
    </div>
  </div>
</template>


<script>
export default {
  name: "mainContainer",

  data: function() {
    return {
      days: ["Mon", "Tues", "Wed", "Thur", "Fri", "Sat", "Sun"]
    };
  },

  props: {
    currDay: Number,
    listOfDays: Array
  },

  methods: {
    setDays: function() {
      this.$emit("setDays");
    },

    selectDay: function(day) {
      alert(`This is ${day} selected`);
    }
  },
  mounted: function() {
    this.setDays();
  }
};
</script>


<style>
#day {
  width: calc(100% / 7);
}

#days-in-month {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: start;
}

li {
  flex-basis: 5%;
}

li.pointer {
  cursor: pointer;
}
</style>