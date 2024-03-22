<template>
    <div class="background">
      <div class="player-container">
        <div v-if="player" class="player-page">
          <div class="player-profile">
            <div v-if="player.image" class="player-image">
              <img :src="player.image.url" :alt="`Image de ${player.first_name} ${player.last_name}`">
            </div>
            <div class="player-details">
              <h1 class="player-name">{{ player.first_name }} {{ player.last_name }}</h1>
              <div class="info-section">
                <div class="player-info">
                  <div class="player-country">
                    <img :src="player.country_player.url" :alt="`Flag of ${player.country}`">{{ player.country }}
                  </div>
                  <div class="player-age">Age: {{ player.age }}</div>
                  <div class="player-description">Description: {{ player.description }}</div>
                </div>
              </div>
              <router-link to="/players" class="back-button">Retourner à la liste des joueurs</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    async asyncData({ params, $axios }) {
      try {
        const { data } = await $axios.get(`/api/players?filters[slug][$eq]=${params.slug}&populate=*`);
        console.log('Joueur récupéré:', data.data[0]);
        return { player: data.data[0] };
      } catch (error) {
        console.error('Erreur lors de la récupération des détails du joueur:', error);
        return { player: null };
      }
    }
  }
  </script>
  <style scoped>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  
  .background {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-image: url("assets/terrain-de-basket.jpg");
    background-size: cover;
  }
  
  .player-container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
  }
  
  .player-page {
    display: flex;
    justify-content: center;
    align-items: center; 
  }
  
  .player-profile {
    display: flex;
    flex-direction: column;
    background-color: rgba(255, 255, 255, 0.8);
    color: black;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
    width: 60%;
    max-width: 800px; 
  }
  
  .player-image img {
    width: 100%;
    height: auto;
    border-radius: 10px;
    margin-bottom: 20px;
  }
  
  .player-details {
    display: flex;
    flex-direction: column;
  }
  
  .player-name {
    margin-bottom: 10px;
    font-size: 2rem;
    text-align: center;
  }
  
  .info-section {
    display: flex;
    align-items: center;
    gap: 20px;
  }
  
  .player-info {
    display: flex;
    flex-direction: column;
  }
  
  .player-country,
  .player-age,
  .player-style,
  .player-description {
    margin: 5px 0;
  }
  
  .player-country img {
    width: 24px;
    height: auto;
    margin-right: 5px;
  }

  .back-button {
  display: inline-block;
  margin-top: 10px; 
  padding: 5px 10px; 
  background-color: #3498db; 
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  transition: background-color 0.3s;
}

.back-button:hover {
  background-color: #2980b9; 
}
</style>
  </style>
  