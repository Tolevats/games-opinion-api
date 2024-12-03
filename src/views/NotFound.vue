<template>
    <div class="not-found-container">
      <h1>404</h1>
      <p>Lo sentimos, la página que buscas no existe.</p>
      <router-link to="/">Volver a Home</router-link>
    </div>
</template>

<script>
export default {
    name: 'NotFound',
    // props: {},
    /* data() {
        return {}
    }, */
    // computed: {},
    //methods: {}
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    // -- End Lifecycle Methods
};
</script>

<style scoped>
.not-found-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  text-align: center;
  color: white;
  padding: 1em;
  box-sizing: border-box;
  background: linear-gradient(to bottom right, #1a1a2e, #16213e, #0f3460); /* Dark gamer theme */
  background-size: 300% 300%;  /* Allows the gradient to shift smoothly */
  animation: gradientShift 10s ease infinite;  /* Gradient animation */
}
h1 {
  font-size: 5em;
  margin: 0 0 0.25em;
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);  /* efecto glow */
}
p {
  font-size: 1.2em;
  margin: 0.5em 0 4em;
}
a {
  text-decoration: none;
  color: #00aaff;
  font-size: 1em;
  border: 2px solid #00aaff;
  padding: 0.5em 0.8em;
  border-radius: 10px;
  transition: background-color 0.3s, color 0.3s;
}
a:hover {
  background-color: #00aaff;
  color: #1a1a2e;
}
/* Animation for the gradient background */
@keyframes gradientShift {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
/* para pantallas más grandes */
@media (min-width: 768px) {
  h1 {
    font-size: 8em;
  }
  p {
    font-size: 1.5em;
  }
  a {
    font-size: 1.2em;
    padding: 0.5em 1em;
  }
}
</style>