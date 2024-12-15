<template>
  <div class="container">
    <div class="chain"></div>
    <div
      v-if="!ko"
      class="bag"
      :class="{ hit: isHit }"
      :style="{ opacity: statusOpacity }"
      @click="hitBag"
    >
      <div class="bag-top"></div>
      <div class="bag-body"></div>
      <div class="bag-bottom"></div>
    </div>
    <div v-if="!ko" class="base"></div>

    <Reset v-if="ko" @reset-game="reset" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Reset from './ResetGame.vue'

let statusOpacity = ref('100%')
let ko = ref(false)
let lifePoints = 100

const isHit = ref(false)

const hitBag = () => {
  if (lifePoints == 20) {
    ko.value = true
  } else {
    lifePoints -= 20
    isHit.value = true
    setTimeout(() => {
      isHit.value = false
    }, 300)
    statusOpacity.value = `${lifePoints}%`
  }
}

function reset() {
  lifePoints = 100
  statusOpacity.value = '100%'
  ko.value = false
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
}

.chain {
  width: 4px;
  height: 100px;
  background-color: #888;
  margin-bottom: -2px;
}

.bag {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.bag-top {
  width: 80px;
  height: 20px;
  background-color: #8b4513;
  border-radius: 40px 40px 0 0;
}

.bag-body {
  width: 150px;
  height: 300px;
  background-color: #a0522d;
  border-radius: 20px;
  position: relative;
  overflow: hidden;
}

.bag-bottom {
  width: 150px;
  height: 30px;
  background-color: #8b4513;
  border-radius: 0 0 75px 75px;
}

.base {
  width: 200px;
  height: 20px;
  background-color: #333;
  margin-top: 20px;
  border-radius: 10px;
}

.hit {
  animation: shake 0.3s ease-in-out;
}

.hit .bag-body::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 0;
  height: 0;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 50%;
  animation: ripple 0.3s ease-out;
}

@keyframes shake {
  0%,
  100% {
    transform: translateX(0);
  }
  25% {
    transform: translateX(-10px) rotate(-5deg);
  }
  75% {
    transform: translateX(10px) rotate(5deg);
  }
}

@keyframes ripple {
  0% {
    width: 0;
    height: 0;
    opacity: 1;
  }
  100% {
    width: 100px;
    height: 100px;
    opacity: 0;
  }
}
</style>
