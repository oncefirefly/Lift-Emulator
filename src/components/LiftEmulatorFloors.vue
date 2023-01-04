<script>
import LiftEmulatorLift from "./LiftEmulatorLift.vue";

export default {
  props: {
    lifts: {
      type: Array,
      required: true,
      default: null,
    },
    floors: {
      type: Array,
      required: true,
      default: null,
    },
  },

  components: {
    LiftEmulatorLift,
  },
};
</script>

<template v-if="floors.length">
  <div class="floors">
    <div v-for="(floor, index) in floors" :key="index" class="floor">
      <button class="floor_btn">{{ floor }}</button>
      <div
        v-for="lift in lifts.filter((lift) => lift.currFloor === floor)"
        :key="lift.id"
        class="lift-container"
      >
        <LiftEmulatorLift />
      </div>
    </div>
  </div>
</template>

<style scoped>
.floors {
  display: flex;
  flex-direction: column-reverse;
}

.floor {
  width: 100vw;
  height: 120px;
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  border-bottom: 1px solid #111;
}

.floor_btn {
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.lift-container:not(:first-child) {
  margin-left: 20px;
}
</style>
