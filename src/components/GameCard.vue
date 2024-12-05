<template>
  <div class="game-card">
    <img :src="game.background_image" alt="Game image" class="game-image"/>
    <div class="game-title">
      <h3>{{ game.name }}</h3>
      <span class="heart-icon">❤️</span>
    </div>
    <p>⭐ <strong>Rating:</strong> {{ game.rating }}</p>
    <p>🗓️ <strong>Released:</strong> {{ game.released }}</p>
    <p>🔄 <strong>Updated:</strong> {{ game.updated }}</p>
    <button @click="$emit('review', game.name)">Review it!</button>
  </div>
</template>

<script>
export default {
  name: 'GameCard',
  props: ['game']
};
</script>

<style scoped>
.game-card {
  border: 1px solid #ccc;
  background: linear-gradient(145deg, #1f1f1f, #292929);
  border-radius: 12px;
  padding: 1em;
  margin: 1.5em;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.6);
  transition: transform 0.3s, box-shadow 0.3s;;
  overflow: hidden;
}
.game-card:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.8);
}

.game-image {
  width: 100%;
  height: auto;
  border-radius: 10px;
  margin-bottom: 0.5em;
}

.game-title {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5em;
}

h3 {
  margin: 0;
  font-size: 1.4em;
  text-align: left;
  flex-grow: 1;
}

.heart-icon {
  font-size: 1.5em;
  cursor: pointer;
  transition: transform 0.3s ease;
}
.heart-icon:hover {
  transform: scale(1.3);
}

p {
  margin: 0.3em 0;
  font-size: 1em;
}

button {
  margin-top: 0.8em;
  padding: 0.8em 1.5em;
  border: none;
  border-radius: 8px;
  background-color: #4CAF50;
  color: white;
  font-size: 1em;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #357a38;
}
</style>