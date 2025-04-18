<template>
  <div class="projects-container">
    <h1>My Projects</h1>
    
    <div class="projects-grid">
      <div 
        v-for="project in projects" 
        :key="project.id" 
        class="project-card"
      >
        <h2>{{ project.name }}</h2>
        <p class="project-description">{{ project.description }}</p>
        <p class="project-tech">
          <span class="tech-label">Technologies:</span> 
          {{ project.technologies }}
        </p>
        <a 
          :href="project.link" 
          target="_blank" 
          class="project-link"
        >
          View Project
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
const projects = [
  {
    id: 1,
    name: "E-commerce Website",
    description: "A full-stack online store with payment integration",
    technologies: "Vue.js, Node.js, MongoDB",
    link: "#"
  },
  {
    id: 2,
    name: "Weather App",
    description: "Displays current weather using OpenWeather API",
    technologies: "JavaScript, API Integration",
    link: "#"
  },
  {
    id: 3,
    name: "Task Manager",
    description: "CRUD application for managing daily tasks",
    technologies: "React, Firebase",
    link: "#"
  }
]
</script>

<style>
.projects-container {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.projects-container h1 {
  font-size: 2rem;
  color: #333;
}

.projects-grid {
  display: grid;
  gap: 1.5rem;
}

@media (min-width: 768px) {
  .projects-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .projects-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

.project-card {
  background-color: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  border: 1px solid #eee;
  transition: box-shadow 0.3s ease;
}

.project-card:hover {
  box-shadow: 0 4px 8px rgba(0,0,0,0.15);
}

.project-card h2 {
  font-size: 1.25rem;
  color: #333;
  margin-bottom: 0.75rem;
}

.project-description {
  color: #666;
  margin-bottom: 1rem;
}

.project-tech {
  margin-bottom: 1.5rem;
}

.tech-label {
  font-weight: 500;
  color: #444;
}

.project-link {
  display: inline-block;
  padding: 0.5rem 1rem;
  background-color: #0066cc;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.project-link:hover {
  background-color: #0052a3;
}
</style>