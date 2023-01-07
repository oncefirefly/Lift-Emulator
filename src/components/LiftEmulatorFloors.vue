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

  methods: {
    getClosestEmptyLiftId(destFloor) {
      return this.lifts
        .filter((lift) => lift.busy !== true) // looking for empty not-busy lift
        .reduce((prev, curr) => {
          // getting the closest lift
          return Math.abs(curr.currFloor - destFloor) <
            Math.abs(prev.currFloor - destFloor)
            ? curr
            : prev;
        }).id;
    },

    callLift(destFloor) {
      // if there's any lift with the same current floor as the destination floor => do nothing
      if (this.lifts.filter((lift) => lift.currFloor === destFloor).length) {
        console.log("I'm chillin");
        return;
      }

      const closestLiftId = this.getClosestEmptyLiftId(destFloor);

      this.lifts.filter((lift) => lift.id === closestLiftId)[0].currFloor =
        destFloor;
    },
  },
};
</script>

<template v-if="floors.length">
  <div class="floors">
    <div v-for="(floor, index) in floors" :key="index" class="floor">
      <button @click="callLift(floor)" class="floor_btn">
        {{ floor }}
      </button>
      <div
        v-for="lift in lifts.filter((lift) => lift.currFloor === floor)"
        :key="lift.id"
        :style="{ position: 'absolute', left: 70 + (lift.id - 1) * 120 + 'px' }"
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
  height: 110px;
  padding: 10px 10px 0 10px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  border-bottom: 1px solid #111;
}

.floor_btn {
  margin-right: 20px;
  width: 30px;
  height: 30px;
  border: none;
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  font-weight: 700;
  color: #111;
  background: #03a1fc;
}
</style>
