<template>
  <div class="VueCarousel-navigation">
    <button
      type="button"
      aria-label="Previous page"
      role="button"
      class="VueCarousel-navigation-button VueCarousel-navigation-prev"
      v-on:click.prevent="triggerPageAdvance('backward')"
      v-bind:class="{ 'VueCarousel-navigation--disabled': !canAdvanceBackward }"
      v-bind:style="`padding: ${clickTargetSize}px; margin-right: -${clickTargetSize}px;`">
      <div class="arrow-left"></div>
    </button>
    <button
      type="button"
      aria-label="Next page"
      role="button"
      class="VueCarousel-navigation-button VueCarousel-navigation-next"
      v-on:click.prevent="triggerPageAdvance()"
      v-bind:class="{ 'VueCarousel-navigation--disabled': !canAdvanceForward }"
      v-bind:style="`padding: ${clickTargetSize}px; margin-left: -${clickTargetSize}px;`">
      <div class="arrow-right"></div>
    </button>
  </div>
</template>

<script>
export default {
  name: "navigation",
  inject: ["carousel"],
  props: {
    /**
     * Amount of padding to apply around the label in pixels
     */
    clickTargetSize: {
      type: Number,
      default: 8
    },
    /**
     * Text content of the navigation next button
     */
    nextLabel: {
      type: String,
      default: "&#9654"
    },
    /**
     * Text content of the navigation prev button
     */
    prevLabel: {
      type: String,
      default: "&#9664"
    }
  },
  computed: {
    /**
     * @return {Boolean} Can the slider move forward?
     */
    canAdvanceForward() {
      return this.carousel.canAdvanceForward || false;
    },
    /**
     * @return {Boolean} Can the slider move backward?
     */
    canAdvanceBackward() {
      return this.carousel.canAdvanceBackward || false;
    }
  },
  methods: {
    /**
     * Trigger page change on +/- 1 depending on the direction
     * @param {"backward"} [direction]
     * @return {void}
     */
    triggerPageAdvance(direction) {
      /**
       * @event paginationclick
       * @type {string}
       */
      this.$emit("navigationclick", direction);
    }
  }
};
</script>

<style scoped>
.VueCarousel-navigation-button {
  height: 100%;
  width: 135px;
  position: absolute;
  top: 50%;
  box-sizing: border-box;
  color: #000;
  text-decoration: none;
  appearance: none;
  border: none;
  background-color: transparent;
  padding: 0;
  cursor: pointer;
  outline: none;
}

.VueCarousel-navigation-next {
  right: 135px;
  transform: translateY(-50%) translateX(100%);
  font-family: "system";
  background: linear-gradient(
    to left,
    rgba(30, 30, 28, 1) 0%,
    rgba(30, 30, 28, 1) 50%,
    rgba(30, 30, 28, 0.8) 70%,
    rgba(30, 30, 28, 0) 100%
  );
}

.VueCarousel-navigation-prev {
  left: 135px;
  transform: translateY(-50%) translateX(-100%);
  font-family: "system";
  background: linear-gradient(
    to right,
    rgba(30, 30, 28, 1) 0%,
    rgba(30, 30, 28, 1) 50%,
    rgba(30, 30, 28, 0.8) 70%,
    rgba(30, 30, 28, 0) 100%
  );
}

.VueCarousel-navigation--disabled {
  opacity: 0;
  cursor: default;
}

.arrow-left {
  width: 0;
  height: 0;
  border-top: 15px solid transparent;
  border-bottom: 15px solid transparent;
  border-right: 15px solid #777777;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 9px;
  margin: auto;
}

.arrow-right {
  height: 0;
  width: 0;
  border-top: 15px solid transparent;
  border-bottom: 15px solid transparent;
  border-left: 15px solid #777777;
  position: absolute;
  top: 0;
  bottom: 0;
  right: 9px;
  margin: auto;
}

/* Define the "system" font family */
@font-face {
  font-family: system;
  font-style: normal;
  font-weight: 300;
  src: local(".SFNSText-Light"), local(".HelveticaNeueDeskInterface-Light"),
    local(".LucidaGrandeUI"), local("Ubuntu Light"), local("Segoe UI Symbol"),
    local("Roboto-Light"), local("DroidSans"), local("Tahoma");
}
</style>
