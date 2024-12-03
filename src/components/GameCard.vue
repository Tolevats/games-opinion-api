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
  border-radius: 10px;
  padding: 1em;
  margin-bottom: 1.5em;
  text-align: center;
  background-color: #f9f9f9;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}
.game-card:hover {
  transform: scale(1.03); /* Slight zoom effect on hover */
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
  padding: 0.6em 1.2em;
  border: none;
  border-radius: 20px;
  background-color: #ff4d4d;
  color: white;
  font-size: 1em;
  cursor: pointer;
  transition: background-color 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

button:hover {
  background-color: #ff3333;
}
</style>