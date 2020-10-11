<template>
  <div class="home">
    <clock :timeZone="timeZoneMap" />
  </div>
</template>

<script>
import Clock from "@/components/Clock.vue";

export default {
  name: "Home",
  props: {
    pageInfo: {
      default: () => ({}),
      type: Object
    }
  },
  computed: {
    timeZoneMap() {
      // https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
      const timeZone =
        {
          cupertino: "America/Los_Angeles",
          "new-york-city": "America/New_York",
          london: "Europe/London",
          amsterdam: "Europe/Amsterdam",
          tokyo: "Asia/Tokyo",
          "hong-kong": "Asia/Hong_Kong",
          sydney: "Australia/Sydney"
        }[this.pageInfo.section] || "America/Los_Angeles";
      return timeZone;
    }
  },
  components: { Clock }
};
</script>

<style lang="sass">
.home
  padding: 50px 0 0
</style>
