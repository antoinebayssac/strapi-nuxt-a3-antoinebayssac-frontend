<template>
  <div class="background-basketball">
    <div class="content">
      <h1>Liste des participants à la compétition de basket - 20 juin 2024</h1>
      <router-link to="/players" class="discover-link">Entrer !</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NuxtTutorial'
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.background-basketball {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-image: url("assets/terrain-de-basket.jpg"); /* Image de basket-ball en arrière-plan */
  background-size: cover;
}

.content {
  text-align: center;
  color: white;
  font-family: Arial, Helvetica, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 20px;
  padding: 20px;
  border-radius: 10px;
  backdrop-filter: blur(5px);
}

.discover-link {
  text-decoration: none;
  border: 2px solid white; /* Bordure blanche */
  padding: 10px 20px; /* Espacement intérieur */
  color: white;
  border-radius: 10px;
  font-size: 18px; /* Taille de police */
  transition: all 0.3s ease-in-out;
}

.discover-link:hover {
  background-color: rgba(255, 255, 255, 0.1); /* Fond semi-transparent au survol */
}
</style>
