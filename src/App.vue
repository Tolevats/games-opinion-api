<template>
  <div id="app">
    <Navbar />
    <router-view />
    <Footer />
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';

export default {
  components: {
    Navbar,
    Footer
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
}

body {
  font-family: 'Montserrat', sans-serif;
  background-color: #121212; /* Fondo oscuro */
  color: #ffffff; /* Texto principal */
  height: 100vh;
}
</style>
