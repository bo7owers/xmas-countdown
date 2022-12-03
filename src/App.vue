<script setup>
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from './components/CountdownSegment.vue'
import { useNow } from '@vueuse/core'
import { computed } from 'vue'

const now = useNow()
const christmas = new Date('12/25/2022 00:00:00')
let daylength = 1000 * 60 * 60 * 24

// console.log(christmas.getTime() - now.value.getTime() / daylength)

// computed props
const daysTo = computed(() => {
  // get complete amount of time left till christmas
  let fullChristmasDay = (christmas.getTime() - now.value) / daylength
  // round it to get a specific amount of days
  let roundChristmasDate = Math.floor((christmas.getTime() - now.value.getTime()) / daylength)
  return { fullChristmasDay, roundChristmasDate }
})
// access the results from daysTo
let fullDaysToChristmas = daysTo.value.fullChristmasDay
let daysToChristmas = daysTo.value.roundChristmasDate

const hoursTo = computed(() => {
  // get full amount of hours left till christmass
  let fullChristmasHours = (fullDaysToChristmas - daysToChristmas) * 24
  // round hours to get specific amount of days
  let roundChristmasHours = Math.floor(fullChristmasHours)
  return { fullChristmasHours, roundChristmasHours }
})
let fullHoursToChristmas = hoursTo.value.fullChristmasHours
let hoursToChristmas = hoursTo.value.roundChristmasHours

const minutesTo = computed(() => {
  // get full amount of minutes left till christmas
  let fullChristmasMins = (fullHoursToChristmas - hoursToChristmas) * 60
  let roundChristmasMins = Math.floor(fullChristmasMins)
  return { fullChristmasMins, roundChristmasMins }
})
let fullMinsToChristmas = minutesTo.value.fullChristmasMins
let minsToChristmas = minutesTo.value.roundChristmasMins

console.log(hoursTo.value)
</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]" aria-live="polite">
        <!-- {{ christmas }} | {{ now }} -->
        {{ christmasDay }}
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment label="days" :number="daysToChristmas" />
          <CountdownSegment label="hours" :number="hoursToChristmas" />
          <CountdownSegment label="minutes" :number="minsToChristmas" />
          <CountdownSegment label="seconds" :number="0" />
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by <a href="https://vueschool.io/" class="underline">Vue School</a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
