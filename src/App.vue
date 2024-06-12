<script setup>
import { ref, computed } from 'vue'

const time = ref(0)
const elapsedTime = ref(0)
let timerRunning = false

const diameter = 290
const outerRad = diameter * 0.4
const innerRad = outerRad / 2
const circumference = 2 * Math.PI * innerRad

const remainingTimeSegment = computed(() => {
  return circumference * (1 - elapsedTime.value / 60)
})

const innerCircleAttrs = {
  r: innerRad,
  'stroke-width': outerRad,
  'stroke-dasharray': `${circumference} ${circumference}`
}

let timerId = null

const updateTimer = () => {
  elapsedTime.value = time.value

  if (time.value > 0) {
    console.log('starting')

    timerId = setInterval(() => {
      elapsedTime.value -= 1

      if (elapsedTime.value <= 0) {
        console.log('stopping')
        time.value = 0
        clearInterval(timerId)
        return
      }
    }, 1000)
  } else {
    clearInterval(timerId)
    return
  }
}

const resetTimer = () => {
  console.log('resetting')
  time.value = 0
  updateTimer()
}
</script>

<template>
  <div id="main-app">
    <header>
      <h1>Visual Timer</h1>
    </header>

    <main>
      <div class="timer-container">
        <div class="timer-container__input">
          <p>Set minutes:</p>
          <input type="number" v-model="time" placeholder="0" min="0" max="60" />
          <button @click="updateTimer">Start</button>
        </div>
        <div>
          <svg
            class="timer-shape"
            version="1.1"
            viewBox="0 0 290 290"
            xmlns="http://www.w3.org/2000/svg"
          >
            <circle :r="outerRad" cx="50%" cy="50%" class="timer-shape__outer-circle" />
            <circle
              class="timer-shape__inner-circle"
              cx="50%"
              cy="50%"
              v-bind="innerCircleAttrs"
              :style="{ 'stroke-dashoffset': remainingTimeSegment }"
            />
          </svg>
        </div>
        <div class="timer-container__toggle-buttons">
          <button>Pause</button>
          <button @click="resetTimer">Reset</button>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
#timer {
  width: var(--timer-width);
  height: var(--timer-height);
  border-radius: 50%;
  background: transparent;
}

.timer-shape {
  width: var(--timer-width);
  height: var(--timer-height);
}

.timer-shape__outer-circle {
  fill: var(--white);
  opacity: 30%;
}

.timer-shape__inner-circle {
  transform: rotate(-90deg);
  transform-origin: 50% 50%;
  stroke: var(--green);
  fill: transparent;
  /* animation: dash 5s linear; */
}

/* @keyframes fill {
  to {
    stroke-dasharray: var(--timer-inner-c) var(--timer-inner-c);
  }
} */
</style>
