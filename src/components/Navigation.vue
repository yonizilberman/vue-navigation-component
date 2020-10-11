<template>
  <div class="navigation">
    <ul class="tabs">
      <li
        v-for="(i, key) in navigationObj"
        :key="key"
        class="tab"
        :class="`tabNumber-${navigationObj.length}`"
        @click="tabClick(key)"
      >
        <span
          class="text"
          :class="{ select: tabIndex === key }"
          :ref="`tab${key}`"
        >
          {{ i.label }}
        </span>
      </li>
    </ul>
    <div class="slider">
      <div
        class="indicator"
        :class="`tabNumber-${navigationObj.length}`"
        :style="{ left: `calc(${leftPosition}px)` }"
      >
        <div class="indicator-bar" :style="{ width: `${width}px` }"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navigation",
  props: {
    navigationObj: {
      default: () => [],
      type: Array
    }
  },
  mounted() {
    this.widthFunction();
    this.$emit("pageChange", this.navigationObj[this.tabIndex]);
    window.addEventListener("resize", this.widthFunction);
  },
  destroyed() {
    window.removeEventListener("resize", this.widthFunction);
  },
  data() {
    return {
      tabIndex: 0,
      width: 100,
      leftPosition: 0
    };
  },
  methods: {
    tabClick(key) {
      this.tabIndex = key;
      this.widthFunction();
      this.$emit("pageChange", this.navigationObj[this.tabIndex]);
    },
    widthFunction() {
      this.$nextTick(() => {
        const tab = this.$refs[`tab${this.tabIndex}`][0];
        this.width = tab.offsetWidth;
        this.leftPosition =
          tab.parentNode.offsetLeft -
          document.querySelector(".navigation").offsetLeft;
      });
    }
  }
};
</script>

<style lang="sass" scoped>
$dark: #1b1b1b
$gray: #b8b8b8
$link: #1ac0da

.navigation
  width
ul.tabs
  padding: 25px 0 8px

li.tab
  display: inline-block
  text-align: center
  box-sizing: border-box
  cursor: pointer
  color: $gray
  & .text
    &:hover
      color: $link
    &.select
      color: $dark
      cursor: default
      user-select: none

.slider
  position: relative
  width: 100%
  height: 1px
  background: $gray

.indicator
  height: 2px
  transition: all 0.33s cubic-bezier(0.38, 0.8, 0.32, 1.07)
  position: absolute

.indicator-bar
  height: 2px
  display: block
  margin: auto
  background: $dark


/* the number of tabs:
 *   for the class `tab`
 *   for the class `indicator` */

@for $i from 1 through 10
  .tabNumber-#{$i}
    width: calc(100% / #{$i})
</style>
