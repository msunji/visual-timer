<script setup>
import { ref } from 'vue'

const minutes = ref()

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
      <div id="timer">
        <div class="timer-inner"></div>
      </div>
      <p>time is {{ minutes }}</p>
      <div>
        <button>Stop</button>
        <button>Clear</button>
      </div>
    </main>
  </div>
</template>
