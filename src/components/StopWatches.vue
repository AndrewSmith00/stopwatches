<template>
  <div class="stopwatches">
    <stop-watch
      v-for="(stopwatchType, index) in stopwatches"
      v-bind:key="index"
      :type="stopwatchType"
    ></stop-watch>
    <div class="add-button__wrapper">
      <div class="add-button__container">
        <button type="button" class="add-button" @click="addStopwatch('hours')">
          <div>ЧАС</div>
          <div class="add-button__plus-icon"> + </div>
        </button>
        <button type="button" class="add-button" @click="addStopwatch('minutes')">
          <div>МИН</div>
          <div class="add-button__plus-icon"> + </div>
        </button>
        <button type="button" class="add-button" @click="addStopwatch('seconds')">
          <div>СЕК</div>
          <div class="add-button__plus-icon"> + </div>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import StopWatch from "./StopWatch.vue";

export default {
  name: "StopWatches",
  components: { StopWatch },
  data() {
    return {
      stopwatches: ["seconds", "minutes", "hours"],
    };
  },
  methods: {
    addStopwatch(stopwatchType) {
      this.stopwatches.push(stopwatchType);
    },
  },
};
</script>

<style lang="scss">
.stopwatches {
  padding-top: 144px;
  padding-bottom: 80px;
  width: 70%;
  margin: auto;
  display: grid;
  grid-template-columns: 33% 33% 33%;
}

.add-button__wrapper {
  display: flex;
  justify-content: center;
  padding-bottom: 45px;
}

.add-button__container {
  width: 225px;
  height: 120px;
  background-color: #696969;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.add-button {
  font-family: 'Courier New', Courier, monospace;
  background-color: #696969;
  border: none;
  color: #fff;
  font-size: 16px;
}

.add-button__plus-icon {
  color: #9e9e9e;
  font-size: 40px;
  cursor: pointer;
  transition: 0.2s;
  &:hover {
    color: #fff;
  }
}

@media screen and (max-width: 1024px) {
  .stopwatches {
    grid-template-columns: 50% 50%;
  }
}

@media screen and (max-width: 768px) {
  .stopwatches {
    grid-template-columns: 100%;
  }
}
</style>
