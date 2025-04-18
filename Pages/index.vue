<template>
  <div class="home-container">
    <div class="profile-section">
      <img 
        src="/image/P1.jpg" 
        alt="Franky Liu" 
        class="profile-image"
      >
      <div class="profile-info">
        <h1>Franky Liu</h1>
        <p>I'm a second-year UP student studying IKS and I love cats</p>
      </div>
    </div>

    <div class="cat-section">
      <h2>Cat Corner</h2>
      <div class="cat-content">
        <div v-if="catImage" class="cat-image-container">
          <img :src="catImage" alt="Random Cat" class="cat-image">
        </div>
        <div class="cat-fact-container">
          <p class="fact-title">Fun fact about cats:</p>
          <p v-if="catFact" class="cat-fact">"{{ catFact }}"</p>
          <p v-else class="loading-message">Loading cat fact...</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      catImage: null,
      catFact: null,
    };
  },
  async mounted() {
    try {
      const [imageResponse, factResponse] = await Promise.all([
        fetch("https://api.thecatapi.com/v1/images/search"),
        fetch("https://meowfacts.herokuapp.com/")
      ]);
      
      const [imageData, factData] = await Promise.all([
        imageResponse.json(),
        factResponse.json()
      ]);
      
      this.catImage = imageData[0].url;
      this.catFact = factData.data[0];
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  },
};
</script>

<style>
.home-container {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.profile-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
}

@media (min-width: 768px) {
  .profile-section {
    flex-direction: row;
    align-items: center;
  }
}

.profile-image {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid white;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

.profile-info h1 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 0.5rem;
}

.profile-info p {
  color: #666;
}

.cat-section {
  background-color: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.cat-section h2 {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 1rem;
}

.cat-content {
  display: grid;
  gap: 1.5rem;
}

@media (min-width: 768px) {
  .cat-content {
    grid-template-columns: 1fr 1fr;
  }
}

.cat-image-container {
  overflow: hidden;
  border-radius: 8px;
}

.cat-image {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 8px;
  transition: transform 0.3s ease;
}

.cat-image:hover {
  transform: scale(1.05);
}

.cat-fact-container {
  display: flex;
  align-items: center;
}

.fact-title {
  font-size: 1.1rem;
  font-weight: 500;
  color: #444;
  margin-bottom: 0.5rem;
}

.cat-fact {
  color: #666;
  font-style: italic;
}

.loading-message {
  color: #888;
}
</style>