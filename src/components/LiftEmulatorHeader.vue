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

  emits: ["addFloor", "addLift", "removeFloor", "removeLift"],
};
</script>

<template>
  <header>
    <h1 class="title">Lift Emulator</h1>
    <div class="btns">
      <button
        @click="this.$emit('addFloor', this.floorsLength + 1)"
        class="btn"
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
        class="btn"
      >
        Add Lift
      </button>
    </div>
    <div class="btns">
      <button @click="this.$emit('removeFloor')" class="btn">
        Remove Floor
      </button>
      <button @click="this.$emit('removeLift')" class="btn">Remove Lift</button>
    </div>
  </header>
</template>

<style scoped>
@import url(../assets/header.css);
</style>
