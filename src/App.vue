<script setup>
import { ref, computed } from 'vue'

const time = ref(0)
const elapsedTime = ref(0)
let timerRunning = false

const remainingTimeSegment = computed(() => {
  let value = 119.32 / (60 / (60 - elapsedTime.value))

  if (value > 0 && !isNaN(value)) {
    return value
  }
  return 0
})
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
            version="1.1"
            width="400"
            height="400"
            viewBox="0 0 400 400"
            xmlns="http://www.w3.org/2000/svg"
          >
            <circle cx="50%" cy="50%" r="40%" id="outer-circle" />
            <circle
              id="inner-circle"
              :style="{ 'stroke-dashoffset': remainingTimeSegment + '%' }"
              cx="50%"
              cy="50%"
              r="19%"
              fill="transparent"
              stroke-width="38%"
              transform="rotate(-90) translate(-400)"
            />
          </svg>
        </div>
        <div>
          <button>Pause</button>
          <button @click="resetTimer">Reset</button>
        </div>
      </div>
    </main>
  </div>
</template>

<style>
#inner-circle {
  stroke: var(--green);
  fill: transparent;
  stroke-dasharray: 119.32% 119.32%;
  animation: fill 5s linear;
}

@keyframes fill {
  to {
    stroke-dasharray: 119.32% 119.32%;
  }
}
</style>
