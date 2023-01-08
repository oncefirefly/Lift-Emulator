<script>
import LiftEmolatorCallBtn from "./LiftEmolatorCallBtn.vue";
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
    LiftEmolatorCallBtn,
  },

  methods: {
    getClosestEmptyLift(destFloor) {
      return this.lifts
        .filter((lift) => lift.busy !== true) // looking for empty not-busy lift
        .reduce((prev, curr) => {
          // getting the closest lift
          return Math.abs(curr.currFloor - destFloor) <
            Math.abs(prev.currFloor - destFloor)
            ? curr
            : prev;
        });
    },

    moveLift(lift) {
      setTimeout(() => {
        lift.currFloor = lift.destFloor;
        lift.resting = true;
        lift.destFloor = -1;

        setTimeout(() => {
          lift.busy = false;
          lift.resting = false;
        }, 3000);
      }, 1000 * lift.distance);
    },

    callLift(e) {
      const destFloor = +e.target.innerHTML;
      // if there's any lift with the same current floor as the destination floor => do nothing
      if (this.lifts.filter((lift) => lift.currFloor === destFloor).length) {
        return;
      }

      const closestLift = this.getClosestEmptyLift(destFloor);

      closestLift.destFloor = destFloor;

      // prevents to call a new lift to existing destination floor
      if (
        this.lifts.filter(
          (lift) =>
            lift.destFloor === closestLift.destFloor &&
            lift.id !== closestLift.id
        ).length
      ) {
        return;
      }

      closestLift.distance = Math.abs(destFloor - closestLift.currFloor);

      closestLift.busy = true;

      this.moveLift(closestLift);
    },
  },
};
</script>

<template v-if="floors.length">
  <div class="floors">
    <div v-for="(floor, index) in floors" :key="index" class="floor">
      <LiftEmolatorCallBtn
        @call-lift="callLift"
        :floor="floor"
        :lifts="lifts"
      />
      <div
        v-for="lift in lifts.filter((lift) => lift.currFloor === floor)"
        :key="lift.id"
        :style="{ position: 'absolute', left: 70 + (lift.id - 1) * 120 + 'px' }"
        class="lift-container"
      >
        <LiftEmulatorLift :lift="lift" />
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url(../assets/floors.css);
</style>
