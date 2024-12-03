<template>
  <div>
    <h1>List of games</h1>
    <div v-if="loading">Loading games...</div>
    <div v-else-if="error">{{ error }}</div>
    <div v-else class="game-gallery">
      <GameCard
        v-for="game in games" 
        :key="game.id" 
        :game="game" 
        @review="goToOpinions"
      />
    </div>
  </div>
</template>

<script>
import GameCard from '@/components/GameCard.vue';

export default {
  name: 'home-view',
  components: { GameCard },
  data() {
    return {
      games: [], //hace fetch de lista de juegos de api
      loading: true, //realiza un seguimiento si los datos aún se están cargando
      error: null, //almacena cualquier mensaje de error si falla la búsqueda
    };
  },
  methods: {
    fetchGames() {
      const API_KEY = '606bdb722c014c1ca36319fcda8888f3';  //api de RAWG
      const url = `https://api.rawg.io/api/games?key=${API_KEY}`;
      
      fetch(url)
        .then(response => {
          if (!response.ok) {
            throw new Error('Error loading games');
          }
          return response.json();
        })
        .then(data => {
          this.games = data.results;  //almacena los juegos obtenidos en el estado local
          this.loading = false; //establece la carga como falsa después de una obtención exitosa
        })
        .catch(error => {
          this.error = error.message; //guarda el mensaje de error
          this.loading = false; //detener la carga incluso si hay un error
        });
    },
    goToOpinions(gameName) {
      this.$router.push({ name: 'Opinions', params: { game: gameName } });
    }
  },
  created() {  //Lifecycle hook
    this.fetchGames();  //llama a la función cuando el componente se monta
  }
};
</script>

<style scoped>
.game-gallery {
  display: flex;
  flex-direction: column;
  gap: 1em;
}

/* Tablet and Larger Screens */
@media (min-width: 768px) {
  .game-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5em;
  }

  .game-card {
    text-align: left;
  }

  h3 {
    font-size: 1.6em;
  }
}

@media (min-width: 1024px) {
  .game-gallery {
    grid-template-columns: repeat(3, 1fr); /* three-column grid */
  }
}
</style>