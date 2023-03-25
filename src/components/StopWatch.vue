<template>
  <div class="stopwatch__wrapper">
    <div class="stopwatch" :class="{ stopwatch_disabled: !isRunning }">
      <div class="stopwatch__time">
        <span v-if="type === 'hours'"> {{ hours }} </span>

        <span v-if="type === 'minutes'">
          {{ minutes }}
        </span>
        <span v-else-if="type === 'hours'"> :{{ minutes }} </span>

        <span v-if="type === 'seconds'"> {{ seconds }} </span>
        <span v-else> :{{ seconds }} </span>

        <span v-if="type === 'seconds'"> :{{ milliseconds }} </span>
      </div>
      <div class="stopwatch__buttons">
        <button
          type="button"
          class="stopwatch__button"
          v-show="!isRunning"
          @click="start"
        >
          <img src="@/assets/img/start-icon.svg" alt="" />
        </button>
        <button class="stopwatch__button" v-show="isRunning" @click="stop">
          <img src="@/assets/img/stop-icon.svg" alt="" />
        </button>
        <button class="stopwatch__button" @click="reset">
          <img src="@/assets/img/reset-icon.svg" alt="" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "StopWatch",
  props: ["type"],
  data() {
    return {
      tens: 0,
      isRunning: false,
      timer: null,
    };
  },
  computed: {
    milliseconds() {
      let milliseconds = this.tens % 100;
      if (milliseconds < 10) {
        milliseconds = "0" + milliseconds;
      }
      return milliseconds;
    },
    seconds() {
      let seconds;
      if (this.type === "seconds") {
        seconds = Math.floor(this.tens / 100);
      } else {
        seconds = Math.floor((this.tens % 6000) / 100);
      }
      if (seconds < 10) {
        seconds = "0" + seconds;
      }
      return seconds;
    },
    minutes() {
      let minutes;
      if (this.type === "minutes") {
        minutes = Math.floor(this.tens / 6000);
      } else {
        minutes = Math.floor((this.tens % 360000) / 6000);
      }
      if (minutes < 10) {
        minutes = "0" + minutes;
      }
      return minutes;
    },
    hours() {
      let hours = Math.floor(this.tens / 360000);
      if (hours < 10) {
        hours = "0" + hours;
      }
      return hours;
    },
  },
  methods: {
    start() {
      this.timer = setInterval(() => this.tens++, 10);
      this.isRunning = true;
    },
    stop() {
      clearInterval(this.timer);
      this.isRunning = false;
    },
    reset() {
      this.tens = 0;
    },
  },
};
</script>

<style lang="scss">
.stopwatch__wrapper {
  display: flex;
  justify-content: center;

  padding-bottom: 45px;
}

.stopwatch {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 225px;
  height: 120px;
  background-color: #696969;
  font-family: "Courier New", Courier, monospace;
  font-size: 22px;
}

.stopwatch__time,
.stopwatch__buttons {
  height: 50%;
  width: 100%;
  display: flex;
  align-items: center;
  color: #fff;
}

.stopwatch__buttons {
  justify-content: space-evenly;
}

.stopwatch__button {
  background-color: transparent;
  border: none;
  cursor: pointer;
  img {
    filter: brightness(0) saturate(100%) invert(100%) sepia(100%) saturate(2%)
      hue-rotate(42deg) brightness(108%) contrast(101%);
  }
}

.stopwatch__time {
  border-bottom: 1px solid #fff;
  justify-content: center;
}

.stopwatch_disabled {
  .stopwatch__time {
    border-bottom: 1px solid #9e9e9e;
    color: #939393;
  }
  .stopwatch__button {
    background-color: transparent;
    border: none;
    cursor: pointer;
    img {
      filter: none
    }
  }
}
</style>
