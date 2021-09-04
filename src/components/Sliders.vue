<template>
  <div class="time_taken_slider display_flex">
    <label for="time-slider">Time Taken</label>
    <input
      type="range"
      name="time-slider"
      min="0.1"
      max="300"
      class="time_input"
      v-model="time"
      @change="getTime"
    />
  </div>
  <!-- array size input slider -->
  <div class="array_size_slider display_flex">
    <label for="array-slider">Array Size</label>
    <input
      type="range"
      name="array-slider"
      min="10"
      max="200"
      class="array_input"
      v-model="size"
      @change="getArraySize"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      size: 0,
      time: 1,
    };
  },
  methods: {
    getArraySize() {
      this.$emit("getarraysize", this.size);
    },
    getTime() {
      this.$emit("gettime", this.time);
    },
  },
};
</script>

<style scoped>
.display_flex {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.display_flex > label {
  font-size: 25px;
  margin-bottom: 15px;
  color: #333;
  font-family: "Roboto", sans-serif;
}
.display_flex > input {
  width: 200px;
  cursor: pointer;
}
</style>
