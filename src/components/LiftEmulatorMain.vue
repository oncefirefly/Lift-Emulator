<script>
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
};
</script>

<template v-if="floors.length">
  <div v-for="(floor, index) in floors" :key="index" class="floors">
    <div class="floor">
      {{ floor }}
      <div v-for="lift in lifts" :key="lift.id" class="lift-container">
        {{ lift }}
      </div>
    </div>
  </div>
</template>
