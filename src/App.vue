<script>
import Timer from "./components/Timer.vue";
import DefaultTimers from "./components/DefaultTimers.vue";

export default {
  components: {
    Timer,
    DefaultTimers,
  },
  data() {
    return {
      timer: {},
    };
  },
  methods: {
    onSetTimer(timer) {
      this.timer = timer;
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="wrapper">
      <default-timers @set:timer="onSetTimer" />
      <timer :minutes="timer.minutes" :seconds="timer.seconds" />
    </div>
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Arial, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

:root {
  --color-gray-100: #f2f2f2;
  --color-gray-300: #7f7f7f;
  --color-gray-500: #7f7f7f;
  --color-gray-700: #595959;
  --color-gray-900: #141414;
}

.container {
  background-color: var(--color-gray-900);
  display: grid;
  height: 100vh;
  place-items: center;
}

.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.button-container {
  display: flex;
}

.button {
  width: 64px;
  height: 64px;
  background-color: var(--color-gray-700);
  border: none;
  border-radius: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* icon */
.button span {
  color: var(--color-gray-100);
  font-size: 4em;
}

.button + .button {
  margin-left: 1em;
}
</style>
