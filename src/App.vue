<script setup>
import { ref } from 'vue'

const minutes = ref(0)

// function setMinutes(mins) {
//   console.log(mins)
//   return;
// }
</script>

<template>
  <div id="main-app">
    <header>
      <h1>Visual Timer</h1>
    </header>

    <main>
      <div>
        <p>Set minutes:</p>
        <input type="number" v-model="minutes" placeholder="0" min="0" max="60" step="1" />
        <button>Go</button>
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
            cx="50%"
            cy="50%"
            r="19%"
            fill="transparent"
            stroke="tomato"
            stroke-width="38%"
            transform="rotate(-90) translate(-400)"
          />
        </svg>
      </div>
      <p>time is {{ minutes }}</p>
      <div>
        <button>Stop</button>
        <button>Clear</button>
      </div>
    </main>
  </div>
</template>
