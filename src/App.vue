<template>
  <div id="app">
    <navigation
      :navigationObj="navigationObj"
      @pageChange="pageInfo = $event"
    />
    <router-view :pageInfo="pageInfo" />
  </div>
</template>

<script>
import Navigation from "@/components/Navigation.vue";
import { cities } from "@/assets/navigation.json";

export default {
  name: "App",
  data() {
    return {
      navigationObj: cities,
      pageInfo: {}
    };
  },
  components: { Navigation }
};
</script>

<style lang="sass">
*
  margin: 0;
  padding: 0;

#app
  max-width: 1250px
  margin: 0 auto
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
</style>
