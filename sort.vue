<template>
  <h1>Sorting Algorithm Visualizer</h1>
  <button @click="bubbleSort()">Bubble Sort</button>
  <button @click="fillArray()">Shuffle</button>

  <div class="container">
    <div
      class="bar"
      v-for="(number, index) in array"
      :key="index"
      :style="{ height: number + 'px' }"
    ></div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      array: [],
      size: 50,
    };
  },
  methods: {
    fillArray() {
      this.array = [];
      for (let i = 0; i < this.size; i++) {
        this.array.push(this.getRndInteger(5, 750));
      }
    },
    getRndInteger(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    sleep() {
      return new Promise((resolve) => setTimeout(resolve, 1));
    },
    async bubbleSort(){
      let len = this.array.length;
      let checked;
      do{
        checked = false;
        for(let i=0; i<len; i++) {
          if (this.array[i] > this.array[i + 1]) {
            let tmp = this.array[i];
            this.array[i] = this.array[i + 1];
            this.array[i + 1] = tmp;
            await this.sleep();
            checked = true;
          }
        }
      } while(checked)
    }
  },
  created() {
    this.fillArray();
  },
};
</script>

<style>
.container {
  width: 100vw;
  position: fixed;
  left: 100px;
  
}

.bar {
  background-color: black;
  display: inline-block;

}
</style>
