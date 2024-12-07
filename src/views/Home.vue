<template>
  <div>
    <h1>List of games</h1>
    <div v-if="loading" class="load">Loading games...</div>
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
      const url = `https://api.rawg.io/api/games?key=${process.env.VUE_APP_API_KEY}`;
      
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
h1 {
  font-size: 2.5em;
  text-align: center;
  color: #4CAF50; /* Verde neón */
  margin: 1em 0 0.1em;
  text-transform: uppercase;
  letter-spacing: 1px;
}
.load {
  font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  font-size: 4em;
  text-align: center;
  color: #ff6f61; /* acento llamativo */
}

.game-gallery {
  display: flex;
  flex-direction: column;
  gap: 1.5em;
  padding: 1em;
}

/* Tablet and Larger Screens */
@media (min-width: 768px) {
  .game-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5em;
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