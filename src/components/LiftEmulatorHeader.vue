<script>
export default {
  props: {
    liftsLength: {
      type: Number,
      required: false,
      default: null,
    },
    floorsLength: {
      type: Number,
      required: false,
      default: null,
    },
  },

  emits: ["addFloor", "addLift"],
};
</script>

<template>
  <header>
    <h1 class="title">Lift Emulator</h1>
    <div class="add-btns">
      <button
        @click="this.$emit('addFloor', this.floorsLength + 1)"
        class="add-floor-btn"
      >
        Add Floor
      </button>
      <button
        @click="
          this.$emit('addLift', {
            id: this.liftsLength + 1,
            busy: false,
            resting: false,
            currFloor: 1,
            destFloor: 0,
            distance: 0,
          })
        "
        class="add-lift-btn"
      >
        Add Lift
      </button>
    </div>
  </header>
</template>

<style scoped>
@import url(../assets/header.css);
</style>
