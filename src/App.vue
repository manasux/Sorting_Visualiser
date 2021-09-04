<template>
  <header>
    <Sliders
      @getarraysize="get_array_size($event)"
      @gettime="get_time($event)"
    ></Sliders>
    <button class="btn btn_shuffle" @click="fillArray()">Shuffle</button>
    <button class="btn btn_sort" @click="bubbleSort()">Bubble Sort</button>
    <button class="btn btn_sort" @click="insertionSort()">
      Insertion Sort
    </button>
  </header>

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
import Sliders from "./components/Sliders.vue";

export default {
  components: {
    Sliders,
  },
  data() {
    return {
      array: [],
      arraySize: 10,
      time_taken: 0.1,
    };
  },
  methods: {
    get_array_size(array_size) {
      this.arraySize = array_size;
    },
    get_time(time) {
      this.time_taken = time;
    },
    fillArray() {
      this.array = [];
      for (let i = 0; i < this.arraySize; i++) {
        this.array.push(this.getRndInteger(5, 750));
      }
    },
    getRndInteger(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },

    // sleep
    sleep() {
      return new Promise((resolve) => setTimeout(resolve, this.time_taken));
    },

    // Bubble Sort
    async bubbleSort() {
      let len = this.array.length;
      let checked;
      do {
        checked = false;
        for (let i = 0; i < len; i++) {
          if (this.array[i] > this.array[i + 1]) {
            let tmp = this.array[i];
            this.array[i] = this.array[i + 1];
            this.array[i + 1] = tmp;
            await this.sleep();
            checked = true;
          }
        }
      } while (checked);
    },

    // Insertion Sort
    async insertionSort() {
      let len = this.array.length;
      let checked;
      do {
        checked = false;
        for (let i = 1; i < len; i++) {
          // Choosing the first element in our unsorted subarray
          let current = this.array[i];
          // The last element of our sorted subarray
          let j = i - 1;
          while (j > -1 && current < this.array[j]) {
            this.array[j + 1] = this.array[j];
            j--;
          }
          this.array[j + 1] = current;
          await this.sleep();
          checked = false;
        }
      } while (checked);
    },
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  overflow: hidden;
}
header {
  height: 15vh;
  width: 100vw;

  display: flex;
  justify-content: space-around;
  align-items: center;
}
.container {
  width: 100vw;
  display: flex;
  justify-content: center;
}

.bar {
  width: 10px;
  background-color: black;
  display: inline-block;
  margin-right: 2px;
}
.btn {
  width: 130px;
  height: 50px;
  font-weight: bold;
  font-size: 15px;
  border: none;
  outline: none;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 3px;
}
.btn:hover {
  transform: translateY(-3px);
}
.btn:active {
  transform: translateY(5px);
}
.btn_shuffle {
  background-color: #ff5151;
  color: #ffffff;
}
.btn_sort {
  background-color: #91cf74;
}
</style>
