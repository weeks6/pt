<template>
  <div class="button-container default-timers">
    <template v-for="(timer, idx) in defaultTimers" :key="idx">
      <button
        class="button button--default-timer"
        @click="() => passTimer(timer)"
      >
        <span class="timer__value timer__hours"> {{ timer.minutes }}: </span>
        <span class="timer__value timer__minutes">
          {{ timer.seconds < 10 ? `0${timer.seconds}` : timer.seconds }}
        </span>
      </button>
    </template>
  </div>
</template>

<script>
const defaultTimers = [
  {
    minutes: 15,
    seconds: 0,
  },
  {
    minutes: 25,
    seconds: 0,
  },
  {
    minutes: 45,
    seconds: 0,
  },
];

export default {
  setup() {
    return {
      defaultTimers,
    };
  },

  methods: {
    passTimer(timer) {
      this.$emit("set:timer", timer);
    },
  },
};
</script>

<style>
.default-timers {
  margin: 0 10px;
  flex-wrap: wrap;
  margin-bottom: 4em;
}

.default-timers .button--default-timer {
  border-radius: 2em;
  display: flex;
  width: auto;
  height: auto;
  padding: 0.5em 1em;
}

.button--default-timer * {
  flex-shrink: 0;
}

.button--default-timer .timer__value {
  font-size: 1.5em;
}
</style>