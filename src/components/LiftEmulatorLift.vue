<script>
export default {
  props: {
    lift: {
      type: Object,
      required: true,
      default: null,
    },
  },

  computed: {
    moveLiftStyle() {
      if (
        this.lift.destFloor > 0 &&
        this.lift.distance > 0 &&
        this.lift.busy &&
        !this.lift.resting
      ) {
        return this.lift.destFloor > this.lift.currFloor
          ? {
              transform: `translateY(${this.lift.distance * 100 * -1}%)`,
              transition: `transform ${
                1000 * this.lift.distance
              }ms ease-in-out`,
            }
          : {
              transform: `translateY(${this.lift.distance * 100}%)`,
              transition: `transform ${
                1000 * this.lift.distance
              }ms ease-in-out`,
            };
      }

      return {};
    },

    rotateArrow() {
      return this.lift.destFloor > this.lift.currFloor
        ? {
            transform: "rotate(180deg)",
          }
        : {};
    },
  },
};
</script>

<template>
  <div
    class="lift"
    :class="{ resting: this.lift.resting }"
    :style="moveLiftStyle"
  >
    <div v-if="lift.busy && !lift.resting" class="lift-distance-pointer">
      {{ lift.destFloor }}
      <img
        class="lift-pointer-arrow"
        src="../assets/img/arrow.svg"
        alt="arrow"
        :style="rotateArrow"
      />
    </div>
  </div>
</template>

<style scoped>
@import url(../assets/lift.css);
</style>
