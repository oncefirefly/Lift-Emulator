<script>
import LiftEmulatorHeader from "./components/LiftEmulatorHeader.vue";
import LiftEmulatorMain from "./components/LiftEmulatorMain.vue";

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

  methods: {
    addFloor(floor) {
      this.floors = [...this.floors, floor];
    },

    addLift(lift) {
      if (this.floors.length) {
        this.lifts = [...this.lifts, lift];
        return;
      }

      alert("Please add floors.");
    },
  },

  watch: {
    floors() {
      console.log(this.lifts.length);
      console.log(this.floors);
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
  />
  <LiftEmulatorMain :floors="floors" :lifts="lifts" />
</template>
