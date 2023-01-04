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
  padding: 0 10px 0 10px;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

.title {
  margin-right: 100px;
}

.add-btns {
  display: flex;
  margin-right: 30px;
}

.add-btns button {
  margin-right: 25px;
  background-color: #03a1fc;
  border: none;
  color: #111;
  border-radius: 5px;
  padding: 10px;
  font-size: 20px;
  font-weight: 600;
}
</style>
