<script setup>
import PunchBag from './components/PunchBag.vue'
</script>

<template>
  <h1 class="text-center text-3xl mt-10">Punch Bag Game</h1>
  <div class="flex justify-center">
    <PunchBag />
    <div v-if="ko"><h1 class="text-4xl">You won!!</h1></div>
  </div>
</template>

<style lang="css" scoped>
.punchbag {
  background-color: red;
  margin: 20px;
  width: 200px;
  height: 300px;
  border-radius: 10px;
}
</style>
