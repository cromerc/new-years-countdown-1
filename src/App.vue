<script setup>
import { onMounted, ref } from "vue";

import CountdownHeader from "@/components/CountdownHeader.vue";
import CountdownSegment from "@/components/CountdownSegment.vue";

const newYears = new Date(new Date().getFullYear() + 1, 0, 1);

const days = ref(0);
const hours = ref(0);
const minutes = ref(0);
const seconds = ref(0);

const updateTimer = () => {
  const today = new Date();

  // get days
  let diff = Math.floor((newYears.getTime() - today.getTime()) / 1000);
  days.value = Math.floor(diff / (3600 * 24));

  // get hours
  diff -= days.value * 3600 * 24;
  hours.value = Math.floor(diff / 3600);

  // get minutes
  diff -= hours.value * 3600;
  minutes.value = Math.floor(diff / 60);

  // get seconds
  diff -= minutes.value * 60;
  seconds.value = Math.floor(diff);
};

onMounted(() => updateTimer());

setTimeout(() => {
  setInterval(() => {
    updateTimer();
  }, 1000);
}, 1000 - new Date().getMilliseconds());
</script>

<template>
  <div class="app-wrapper">
    <div class="countdown-box">
      <CountdownHeader />
      <main class="flex justify-center">
        <CountdownSegment data-test="days" label="days" :number="days" />
        <CountdownSegment data-test="hours" label="hours" :number="hours" />
        <CountdownSegment data-test="minutes" label="minutes" :number="minutes" />
        <CountdownSegment data-test="seconds" label="seconds" :number="seconds" />
      </main>
    </div>
  </div>
</template>

<style scoped>
.app-wrapper {
  @apply flex items-center justify-center w-full h-full p-10;
}

.countdown-box {
  @apply shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px];
}

body {
  @apply bg-gray-100;
}
</style>
