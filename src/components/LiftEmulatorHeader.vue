<script>
export default {
  props: {
    lifts: {
      type: Array,
      required: false,
      default: null,
    },
    floors: {
      type: Array,
      required: false,
      default: null,
    },
  },

  emits: {
    addFloor: (floor) => typeof floor === "number",
    addLift: (lift) => typeof lift === "object",
  },

  data() {
    return {
      floor: this.floors.length || 1,
      lift: {
        id: this.lifts.length,
        busy: false,
        currFloor: 0,
      },
    };
  },
};
</script>

<template>
  <header>
    <h1>Lift Emulator</h1>
    <div class="add-btns">
      <button @click="this.$emit('addFloor', this.floor)" class="add-floor-btn">
        Add Floor
      </button>
      <button @click="this.$emit('addLift', this.lift)" class="add-lift-btn">
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
