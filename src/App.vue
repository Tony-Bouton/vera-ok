<template>
  <nav>
    <router-link to="/">Home</router-link>
    <router-link to="/api/restaurants/create">create</router-link>
    <router-link to="/api/restaurants/index">liste</router-link>
  </nav>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
  display: flex;
  justify-content: space-around;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  display: flex;
  justify-content: space-around;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
