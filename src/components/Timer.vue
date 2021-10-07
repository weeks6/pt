<template>
  <div class="timer">
    <span class="timer__value timer__hours"> {{ timer.minutes }} : </span>
    <span class="timer__value timer__minutes">
      {{ _seconds }}
    </span>
  </div>

  <div class="button-container">
    <button class="button button--pause" v-if="ticking" @click="pauseTimer">
      <span class="material-icons-round"> pause </span>
    </button>
    <button class="button button--play" v-else @click="playTimer">
      <span class="material-icons-round"> play_arrow </span>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    minutes: {
      type: Number,
      default: 25,
    },
    seconds: {
      type: Number,
      default: 0,
    },
  },
  watch: {
    minutes() {
      this.timer.minutes = this.minutes;
      this.timer.seconds = this.seconds;
      this.pauseTimer();
    },
  },
  methods: {
    time() {
      if (this.timer.seconds === 0 && this.timer.minutes) {
        this.timer.seconds = 60;
        this.timer.minutes -= 1;
      }
      this.timer.seconds -= 1;
    },
    pauseTimer() {
      clearTimeout(this.timeout);
      this.ticking = false;
    },

    playTimer() {
      this.time();
      this.ticking = true;

      this.timeout = setInterval(() => {
        this.time();

        if (this.timer.seconds === 0 && this.timer.minutes) {
          this.timer.seconds = 59;
          this.timer.minutes -= 1;
        }

        if (this.timer.seconds === 0 && this.timer.minutes === 0) {
          this.pauseTimer();
        }
      }, 1000);
    },
  },
  data() {
    return {
      timer: {
        minutes: this.minutes,
        seconds: this.seconds,
      },
      timeout: null,
      ticking: false,
    };
  },
  computed: {
    _seconds() {
      if (this.timer.seconds < 10) {
        return `0${this.timer.seconds}`;
      }

      return this.timer.seconds;
    },
  },
};
</script>

<style>
.timer {
  margin-bottom: 2em;
}

.timer__value {
  font-family: "Open Sans", sans-serif;
  font-size: 4em;
  font-weight: 700;
  color: var(--color-gray-100);
  letter-spacing: 0.05em;
}
</style>
