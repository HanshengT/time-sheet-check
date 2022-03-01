<template>
  <div>
    <p class="title">Time Sheet Check</p>
    <div
      class="one-day"
      v-for="(day, index) in days"
      :key="index"
      :class="pickColor(index)"
    >
      <span>{{ index + 1 }}. </span>
      <div class="time-item">
        <a-input
          v-model="day.start"
          placeholder="Work Start"
          style="width: 60%; margin-right: 8px"
        />
        <a-radio-group v-model="day.startSuffix">
          <a-radio-button value="AM"> AM </a-radio-button>
          <a-radio-button value="PM"> PM </a-radio-button>
        </a-radio-group>
      </div>
      <div class="time-item">
        <a-input
          v-model="day.end"
          placeholder="Work End"
          style="width: 60%; margin-right: 8px"
        />
        <a-radio-group v-model="day.endSuffix">
          <a-radio-button value="AM"> AM </a-radio-button>
          <a-radio-button value="PM"> PM </a-radio-button>
        </a-radio-group>
      </div>
      <div class="time-item day-total-time">
        <span>{{
          calcOneDayHour(
            day.start,
            day.end,
            day.startSuffix,
            day.endSuffix,
            index
          )
        }}</span>
      </div>
    </div>
    <span class="total-hours">Total Hours: {{ calcTotalHours() }}</span>
    <p class="footer">Powered by Hansen Tao</p>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "TimeSheetCheck",
  data() {
    return {
      numberOfDays: 31,
      days: [],
    };
  },
  created() {
    this.createDays();
    // console.log(this.days);
  },
  methods: {
    createDays() {
      for (let i = 0; i < this.numberOfDays; i++) {
        this.days.push({
          start: "",
          startSuffix: "AM",
          end: "",
          endSuffix: "PM",
          hours: 0,
        });
      }
    },
    calcOneDayHour(start, end, startSuffix, endSuffix, index) {
      let startMoment = moment(
        `${start}-${startSuffix}`,
        ["hhmm-A", "hmm-A", "h-A", "hh-A"],
        true
      );
      let endMoment = moment(
        `${end}-${endSuffix}`,
        ["hhmm-A", "hmm-A", "h-A", "hh-A"],
        true
      );
      let hours = endMoment.diff(startMoment, "hour", true);

      //   if (start) console.log(startMoment);
      //   if (end) console.log(endMoment);

      if (!hours) {
        this.days[index].hours = 0;
        return "----";
      }
      // console.log(endMoment.diff(startMoment, 'hour', true))

      this.days[index].hours = hours;

      return hours;
    },
    calcTotalHours() {
      let totalHours = 0;
      this.days.forEach((day) => {
        totalHours += day.hours;
      });
      // console.log(totalHours);
      return totalHours;
    },
    pickColor(index) {
      //   console.log(index % 2)
      return !(index % 2) ? "hasColor" : "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.title {
  font-size: 32px;
  padding: 24px;
  font-weight: 600;
}

.one-day {
  padding: 10px;
  box-shadow: 0 -2px 4px #cdcdcd;
}
.hasColor {
  background-color: #ecf6ff;
}

.time-item {
  display: inline-block;
}

.day-total-time {
  background-color: #ffffff;
  margin-left: 30px;
  padding: 5px;
  border: 1px solid rgb(217, 217, 217);
  border-radius: 4px;
  min-width: 50px;
}
.total-hours {
  font-size: 30px;
  position: fixed;
  top: 10vh;
  right: 3vw;
}

.footer {
    font-weight: 600;
    color: #aca9a9;
    padding: 16px;
}
</style>
