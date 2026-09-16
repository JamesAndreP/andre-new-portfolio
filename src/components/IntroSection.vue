<script setup lang="ts">
import { ref, onMounted } from 'vue'

const firstLineText = ref('')
const secondLineText = ref('')
const thirdLineText = ref('')
const showCursor = ref(true)
const firstLineFull = "Hi, I'm James"
const secondLineFull = 'A Full Stack Web'
const thirdLineFull = 'Developer'
const colorClasses = ['red', 'blue', 'yellow', 'green', 'purple', 'pink', 'cyan', 'orange']
const getCharColor = (index: number) => {
  return colorClasses[index % colorClasses.length]
}

const typeText = async () => {
  // Type first line
  for (let i = 0; i < firstLineFull.length; i++) {
    firstLineText.value += firstLineFull[i]
    await new Promise((resolve) => setTimeout(resolve, 100))
  }
  // Wait a bit before second line
  await new Promise((resolve) => setTimeout(resolve, 300))
  // Type second line
  for (let i = 0; i < secondLineFull.length; i++) {
    secondLineText.value += secondLineFull[i]
    await new Promise((resolve) => setTimeout(resolve, 100))
  }
  // Wait a bit before third line
  await new Promise((resolve) => setTimeout(resolve, 300))
  // Type third line
  for (let i = 0; i < thirdLineFull.length; i++) {
    thirdLineText.value += thirdLineFull[i]
    await new Promise((resolve) => setTimeout(resolve, 100))
  }
}

onMounted(() => {
  typeText()
})
</script>
<template>
  <div class="intro-main">
    <div class="wrapper">
      <div class="intro-container">
        <div class="dev-logo-container">
          <img src="../assets/img/james-dev-logo.png" alt="Dev Logo" />
        </div>
        <div class="align-center">
          <span
            v-for="(char, index) in firstLineText"
            :key="'first-' + index"
            :class="getCharColor(index)"
            >{{ char }}</span
          >
          <span v-if="showCursor && firstLineText.length < firstLineFull.length" class="cursor"
            >┃</span
          >
        </div>
        <div class="align-center">
          <span
            v-for="(char, index) in secondLineText"
            :key="'second-' + index"
            :class="getCharColor(index)"
            >{{ char }}</span
          >
          <span
            v-if="
              showCursor &&
              firstLineText.length === firstLineFull.length &&
              secondLineText.length < secondLineFull.length
            "
            class="cursor"
            >┃</span
          >
        </div>
        <div class="align-center">
          <span
            v-for="(char, index) in thirdLineText"
            :key="'third-' + index"
            :class="getCharColor(index)"
          >
            <template v-if="index === 0 && char === 'D'">
              <img src="../assets/img/dre-primary-logo.png" alt="D" class="dre-logo" />
            </template>
            <template v-else>{{ char }}</template>
          </span>
          <span
            v-if="
              showCursor &&
              firstLineText.length === firstLineFull.length &&
              secondLineText.length === secondLineFull.length
            "
            class="cursor"
            >┃</span
          >
        </div>
      </div>
    </div>
  </div>
</template>
