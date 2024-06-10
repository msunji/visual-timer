<script setup>
import { ref, computed } from 'vue'

const time = ref(0)
const elapsedTime = ref(0)
const remainingTime = computed(() => {
  return 119.32 / (60 / (60 - elapsedTime.value))
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
        clearInterval(timerId)
      }
    }, 60000)
  }
}

const stopTimer = () => {
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
      <div>
        <p>Set minutes:</p>
        <input type="number" v-model="time" placeholder="0" min="0" max="60" />
        <button @click="updateTimer">Go</button>
        <p style="color: white">{{ elapsedTime }}</p>
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
            :style="{ 'stroke-dashoffset': remainingTime + '%' }"
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
        <button @click="stopTimer">Stop and Reset</button>
      </div>
    </main>
  </div>
</template>

<style>
#inner-circle {
  stroke: tomato;
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
