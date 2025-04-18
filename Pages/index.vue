<!-- Franky Liu 24673898 -->
<template>
  <div class="space-y-8">
    <div class="flex flex-col md:flex-row gap-8 items-center">
      <img 
        src="/image/P1.jpg" 
        alt="Franky Liu" 
        class="w-32 h-32 md:w-48 md:h-48 rounded-full object-cover border-4 border-white shadow-md"
      >
      <div>
        <h1 class="text-3xl font-bold text-gray-800">Franky Liu</h1>
        <p class="mt-2 text-gray-600">I'm a second-year UP student studying IKS and I love cats</p>
      </div>
    </div>

    <!-- Cat API Section -->
    <div class="bg-white p-6 rounded-lg shadow-md">
      <h2 class="text-xl font-semibold text-gray-800 mb-4">Cat Corner</h2>
      <div class="grid md:grid-cols-2 gap-6">
        <div v-if="catImage" class="overflow-hidden rounded-lg">
          <img 
            :src="catImage" 
            alt="Random Cat" 
            class="w-full h-64 object-cover rounded-lg hover:scale-105 transition-transform"
          >
        </div>
        <div class="flex items-center">
          <div>
            <p class="text-lg font-medium text-gray-700 mb-2">Fun fact about cats:</p>
            <p v-if="catFact" class="text-gray-600 italic">"{{ catFact }}"</p>
            <p v-else class="text-gray-500">No cat fact available</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// This will run during static generation
const { data: catData } = await useAsyncData('cats', async () => {
  try {
    const [imageResponse, factResponse] = await Promise.all([
      $fetch("https://api.thecatapi.com/v1/images/search"),
      $fetch("https://meowfacts.herokuapp.com/")
    ]);
    
    return {
      catImage: imageResponse[0]?.url,
      catFact: factResponse?.data?.[0] || "Cats are awesome!"
    };
  } catch (error) {
    console.error("Error fetching cat data:", error);
    return {
      catImage: null,
      catFact: "Couldn't load cat facts right now"
    };
  }
});

const catImage = ref(catData.value?.catImage);
const catFact = ref(catData.value?.catFact);
</script>