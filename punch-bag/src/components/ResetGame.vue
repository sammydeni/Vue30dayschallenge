<script setup>
const emits = defineEmits(['resetGame'])
</script>
<template>
  <h1 class="text-5xl mt-10">You won!!</h1>
  <div class="resetBtn" @click="emits('resetGame')">Reset</div>
</template>

<style lang="css" scoped>
.resetBtn {
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 16px;
  color: #fff;
  background-color: #0070f3;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.resetBtn:hover {
  background-color: #0051a2;
}
</style>
