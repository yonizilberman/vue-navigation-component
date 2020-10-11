<template>
  <div class="clock">
    <div>
      <h1>{{ dateObj.fullDate }}</h1>
      <h3>{{ dateObj.time }} {{ dateObj.amfm }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: "Clock",
  mounted() {
    this.timer = setInterval(() => {
      let formatter = new Intl.DateTimeFormat([], {
        timeZone: this.timeZone,
        year: "numeric",
        month: "numeric",
        day: "numeric",
        hour: "numeric",
        minute: "numeric",
        second: "numeric"
      });
      this.dateObj = this.parseTime(formatter.format(new Date()));
    }, 1000);
  },
  destroyed() {
    clearInterval(this.timer);
  },
  props: {
    timeZone: {
      default: "",
      type: String
    }
  },
  data() {
    return {
      timer: null,
      dateObj: {}
    };
  },
  methods: {
    parseTime(date) {
      let [fullDate, time, amfm] = date.split(" ");
      fullDate = fullDate.replace(",", "");
      return { fullDate, time, amfm };
    }
  }
};
</script>

<style lang="sass">
.clock
  width: 250px
  height: 250px
  margin: auto
  text-align: center
  background: #f6f6f6
  position: relative
  & > div
    padding: 80px 0
    box-sizing: border-box
</style>
