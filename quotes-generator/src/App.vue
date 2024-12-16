<script setup>
import { ref } from 'vue'
import { ContentLoader } from 'vue-content-loader'

const isLoading = ref(true)

const quote = ref({
  quoteText: '',
  author: '',
})

async function updateQuote() {
  isLoading.value = true
  // Fetch a random quote from the Quotable API
  const response = await fetch('https://api.quotable.io/random')
  const data = await response.json()
  if (response.ok) {
    // Update DOM elements
    setTimeout(() => {
      quote.value.quoteText = data.content
      quote.value.author = data.author
      isLoading.value = false
    }, 1000)
  } else {
    quote.value.quoteText = 'An error occured'
    console.log(data)
  }
}
</script>
<template>
  <h1 class="text-center text-3xl m-5">Quote Generator</h1>
  <div class="flex flex-col">
    <div class="box">
      <ContentLoader v-if="isLoading">
        speed={2} width={340} height={84} viewBox="0 0 340 84" backgroundColor="#f3f3f3"
        foregroundColor="#ecebeb" >
        <rect x="0" y="0" rx="3" ry="3" width="67" height="11" />
        <rect x="76" y="0" rx="3" ry="3" width="140" height="11" />
        <rect x="127" y="48" rx="3" ry="3" width="53" height="11" />
        <rect x="187" y="48" rx="3" ry="3" width="72" height="11" />
        <rect x="18" y="48" rx="3" ry="3" width="100" height="11" />
        <rect x="0" y="71" rx="3" ry="3" width="37" height="11" />
        <rect x="18" y="23" rx="3" ry="3" width="140" height="11" />
        <rect x="166" y="23" rx="3" ry="3" width="173" height="11" />
      </ContentLoader>
      <div v-if="!isLoading">
        <h1 class="text-center text-4xl">{{ quote.quoteText }}</h1>
        <h1 class="text-center text-xl mt-2 italic">{{ quote.author }}</h1>
      </div>
    </div>
    <div class="btn self-center mt-4" @click="updateQuote">Generate</div>
  </div>
</template>
<style lang="css" scoped>
.box {
  align-self: center;
  width: 80vw;
  border: 1px solid grey;
  border-radius: 15px;
  padding: 15px;
}

.btn {
  width: 200px;
  background-color: #007bff; /* Blue background color */
  color: white; /* White text color */
  border: none; /* Remove default border */
  padding: 10px 20px; /* Add padding */
  text-align: center; /* Center text */
  text-decoration: none; /* Remove underline from text */
  font-size: 16px; /* Set font size */
  cursor: pointer; /* Add cursor pointer on hover */
  border-radius: 5px; /* Add rounded corners */
  transition: all 0.3s ease; /* Add smooth transition for hover effects */
}

.btn:hover {
  background-color: #0056b3; /* Darker blue on hover */
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.2); /* Add a subtle shadow on hover */
}

.btn:active {
  transform: translateY(1px); /* Slightly move the button down on click */
}
</style>
