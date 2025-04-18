<template>
  <div class="app-container">
    <NuxtRouteAnnouncer />
    <nav class="main-nav">
      <NuxtLink to="/" class="nav-link" active-class="active-link">
        Home
      </NuxtLink>
      <NuxtLink to="/contact" class="nav-link" active-class="active-link">
        Contact
      </NuxtLink>
      <NuxtLink to="/project" class="nav-link" active-class="active-link">
        Projects
      </NuxtLink>
    </nav>
    <main class="main-content">
      <NuxtPage />
    </main>
  </div>
</template>

<style>
.app-container {
  min-height: 100vh;
  background-color: #f5f5f5;
}

.main-nav {
  background-color: white;
  padding: 1rem;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  display: flex;
  gap: 1.5rem;
  justify-content: center;
}

.nav-link {
  color: #333;
  text-decoration: none;
  padding: 0.5rem;
}

.nav-link:hover {
  color: #0066cc;
}

.active-link {
  color: #0066cc;
  font-weight: bold;
}

.main-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem 1rem;
}
</style>