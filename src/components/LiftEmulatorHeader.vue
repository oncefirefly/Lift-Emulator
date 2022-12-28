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
    <h1>Lift Emulator</h1>
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
            currFloor: 1,
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
header {
  padding: 0 1rem 0 1rem;
  border-bottom: 3px solid #cbd5e1;
  margin-bottom: 4rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.add-btns {
  display: flex;
  margin-right: 1rem;
}

.add-btns button {
  margin-right: 1rem;
  background-color: #8b5cf6;
  border: 1px solid #8b5cf6;
  color: white;
  border-radius: 5px;
  padding: 0.5rem 1.25rem;
  cursor: pointer;
}
</style>
