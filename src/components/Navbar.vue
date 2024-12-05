<template>
  <header>
    <div class="brand">
      <img src="@/assets/icons8-game-100.png" alt="Game Icon" class="brand-icon"/>
      <h1>Games Opinion</h1>
    </div>
    <nav>
      <div class="left-links">
        <router-link to="/">Home</router-link>
      </div>
      <div class="right-links">
        <router-link to="/admin">
          <i class="fas fa-user"></i>My account
        </router-link>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'component-navbar',
};
</script>

<style scoped>
/* header {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #ffbb00;
  color: #333;
  padding: 1em;
}
 */
.brand {
  display: flex;
  align-items: center;
  gap: 0.5em;
  background-color: #4CAF50;
  padding: 1em 2em;
}

.brand-icon {
  width: 3em;
  height: 3em;
}

nav {
  display: flex;
  justify-content: space-between;
  width: 100%;
  background-color: #1f1f1f;
  padding: 1em 2em;
}

.left-links, .right-links {
  display: flex;
  gap: 1em;
  display: inline;
  margin: 0 1.5em 0;
}

a {
  color: white;
  text-decoration: none;
  transition: color 0.3s;
}

/* Hover effect for links */
a:hover {
  color: #4CAF50;
}

/* Home icon styling */
.home-icon {
  margin-right: 0.5em;
  font-size: 1.3em;
}

/* Mobile-first approach */
@media (max-width: 768px) {
  nav {
    flex-direction: column;
    align-items: flex-start;
  }

  .nav-left,
  .nav-right {
    width: 100%;
    justify-content: space-between;
    margin-bottom: 0.5em;
  }

  .nav-right {
    justify-content: flex-end;
  }

  a {
    margin: 0.5em 0; /* Adds spacing between vertical links */
  }
}
</style>