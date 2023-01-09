<script>
import LiftEmulatorHeader from "./components/LiftEmulatorHeader.vue";
import LiftEmulatorMain from "./components/LiftEmulatorFloors.vue";

export default {
  name: "LiftEmulator",

  components: {
    LiftEmulatorHeader,
    LiftEmulatorMain,
  },

  data() {
    return {
      lifts: [],
      floors: [],
    };
  },

  mounted() {
    this.lifts = JSON.parse(localStorage.getItem("lifts")) || [
      {
        id: 1,
        busy: false,
        resting: false,
        currFloor: 1,
        destFloor: 0,
        distance: 0,
      },
    ];
    this.floors = JSON.parse(localStorage.getItem("floors")) || [1, 2, 3, 4, 5];
  },

  methods: {
    addFloor(floor) {
      this.floors = [...this.floors, floor];
    },

    addLift(lift) {
      if (this.floors.length) {
        this.lifts = [...this.lifts, lift];
        return;
      }
    },

    removeFloor() {
      this.floors.pop();
    },

    removeLift() {
      this.lifts.pop();
    },
  },

  watch: {
    lifts: {
      handler() {
        localStorage.setItem("lifts", JSON.stringify(this.lifts));
      },
      deep: true,
    },

    floors: {
      handler() {
        localStorage.setItem("floors", JSON.stringify(this.floors));
      },
      deep: true,
    },
  },
};
</script>

<template>
  <LiftEmulatorHeader
    :liftsLength="lifts.length"
    :floorsLength="floors.length"
    @add-floor="addFloor"
    @add-lift="addLift"
    @remove-floor="removeFloor"
    @remove-lift="removeLift"
  />
  <LiftEmulatorMain :floors="floors" :lifts="lifts" />
</template>
