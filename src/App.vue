<script setup>
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from './components/CountdownSegment.vue'
import { useNow } from '@vueuse/core'
import { computed } from 'vue'

const now = useNow()
const christmas = new Date('12/25/2022 00:00:00')
let daylength = 1000 * 60 * 60 * 24

console.log(christmas.getTime() - now.value.getTime() / daylength)

const timeTo = computed(() => {
  return (christmas.getTime() - now.value.getTime()) / daylength
})

console.log(timeTo)

const daysTo = computed(() => {
  return Math.floor(timeTo.value)
})
</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]">
        <!-- {{ christmas }} | {{ now }} -->
        <!-- {{ daysTo }} -->
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment label="days" :number="daysTo" />
          <CountdownSegment label="hours" :number="0" />
          <CountdownSegment label="minutes" :number="0" />
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
