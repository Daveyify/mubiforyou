<template>
  <nav class="navbar">
    <router-link to="/" class="logo">MUBI4U</router-link>
    <span class="slogan">Descubre las mejores películas</span>
  </nav>
</template>

<script>
export default { name: 'NavBar' }
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 32px;
  background-color: #151558;
  position: sticky;
  top: 0;
  z-index: 100;
}

.logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: #ffffff;
  text-decoration: none;
  font-family: "Climate Crisis", sans-serif;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  font-variation-settings:
    "YEAR" 1979;
}

.slogan {
  color: #ffffff;
  font-size: 0.9rem;
  font-weight: bold;
}

@media (max-width: 600px) {
  .slogan {
    display: none;
  }

  .navbar {
    padding: 12px 16px;
  }
}
</style>