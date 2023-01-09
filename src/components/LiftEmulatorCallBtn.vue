<script>
export default {
  props: {
    floor: {
      type: Number,
      required: true,
      default: null,
    },
    lifts: {
      type: Array,
      required: false,
      default: null,
    },
  },

  emits: ["tryCallLift"],

  computed: {
    floorBtnStyle() {
      return this.lifts.filter((lift) => lift.destFloor === this.floor).length
        ? { background: "#FF6B6B" }
        : { background: "#03a1fc" };
    },
  },
};
</script>

<template>
  <button
    @click="(e) => this.$emit('tryCallLift', e)"
    class="call-btn"
    :style="floorBtnStyle"
  >
    {{ floor }}
  </button>
</template>

<style scoped>
@import url(../assets/callBtn.css);
</style>
