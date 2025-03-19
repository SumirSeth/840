<template>
  <Title>Life in Months</Title>
  <meta name="description" content="Visualize your life in months, assuming a 70-year lifespan.">
  <meta property="og:title" content="Life in Months Visualization">
  <meta property="og:description" content="Visualize your life in months, assuming a 70-year lifespan.">
  <meta author="Sumir Seth">
  <Meta name="description" content="Visualize your life in months, assuming a 70-year lifespan."/>
  <Meta property="og:title" content="Life in Months Visualization"/>
  <Meta property="og:description" content="Visualize your life in months, assuming a 70-year lifespan."/>
  <Meta author="Sumir Seth"/>
  <Link rel="icon" href="/favicon.png" />
  <div>
    <div class="font-['Geist'] bg-black min-h-screen text-white p-8">
      <div class="max-w-5xl mx-auto">
        <div class="mb-6"> 
          <h1 class="text-4xl font-bold ">Life in Months</h1>
          <p class="opacity-40">Assuming average age to be 70 years old.</p>
        </div>
        
        <!-- Age Input Section -->
        <div v-if="!age" class="mb-8">
          <label class="block mb-2">Enter your age:</label>
          <input
            v-model="inputAge"  
            type="number"           
            class="bg-gray-800 px-4 py-2 rounded"
            min="0"
            max="100"
            @keydown.enter="setAge"
          >
          <button 
            class="ml-4 bg-white text-black px-4 py-2 rounded hover:bg-gray-200"
            @click="setAge"
            
          >
            Visualize
          </button>
        </div>

        <!-- Months Visualization -->
        <div v-if="age" class="grid grid-cols-28 gap-2 sm:gap-3 md:gap-4 lg:gap-4">
          <div 
            v-for="month in 840" 
            :key="month"
            :class="[
              'w-2 h-2 lg:w-3 lg:h-3 rounded-sm',
              month <= (age * 12) ? 'bg-white' : 'bg-gray-800',
              month === 840 ? 'bg-red-400' : 'bg-gray-800',
              month === 1 ? 'bg-green-400' : 'bg-gray-800',
            ]"
            :title="`Month ${month}`"
          />
        </div>

        <div v-if="age" class="mt-8">
          <p class="text-lg">
            You've lived approximately {{ (age * 12).toLocaleString() }} months out of 840 months.
          </p>
          <p>
            Past: 
            <span class="text-white">{{ (age * 12) }}</span>
            |
            Future: 
            <span class="text-white">{{ 840 - (age * 12) }}</span>
            |
            <span class="text-white">
              {{ (((age * 12)/(840))*100).toFixed(2) }}% lived.
            </span>
          </p>
          <button
          class="mt-4 bg-white text-black px-4 py-2 rounded hover:bg-gray-200" 
            @click="reset" 
            
          >
            Reset
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>

const age = ref(null)
const inputAge = ref('')

onMounted(() => {
  if(localStorage.getItem('age')) {
    age.value = parseInt(localStorage.getItem('age'))
  }
})


const setAge = () => {
  if (inputAge.value >= 0 && inputAge.value <= 100) {
    age.value = parseInt(inputAge.value)
    localStorage.setItem('age', age.value)
  }
}

const reset = () => {
  age.value = null
  inputAge.value = ''
  localStorage.removeItem('age')
}
</script>

<style>
.grid-cols-12 {
  grid-template-columns: repeat(12, minmax(0, 1fr));
}

::-webkit-scrollbar {
  width: 0rem;
}

::-webkit-scrollbar-track {
  background-color: transparent;
}

::-webkit-scrollbar-thumb {
  background-color: rgba(255, 255, 255, 0.3);
  border-radius: 0.5rem;
}

::-webkit-scrollbar-thumb:hover {
  background-color: rgba(255, 255, 255, 0.5);
}


</style>
