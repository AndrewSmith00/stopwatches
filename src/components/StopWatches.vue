<template>
  <div class="stopwatches">
    <stop-watch
      v-for="(stopwatchType, index) in stopwatches"
      v-bind:key="index"
      :type="stopwatchType"
    ></stop-watch>
    <div class="add-button__wrapper">
      <button type="button" class="add-button" @click="addStopwatch('hours')">
        <span class="add-button__plus-icon"> + </span>
      </button>
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

.add-button {
  width: 225px;
  height: 120px;
  background-color: #696969;
  border: none;
  font-size: 40px;
}

.add-button__plus-icon {
  color: #9e9e9e;
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
