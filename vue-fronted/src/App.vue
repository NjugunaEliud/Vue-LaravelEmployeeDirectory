<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link :to="{name:'empoyeesview'}">Employees</router-link>
    <router-link :to="{name:'register'}">Register</router-link>
  </nav>
  
  <router-view/>
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
  background: white;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
  padding: 12px;
}

nav a.router-link-exact-active {
  color: #42b983;
}
h3{
  color:crimson;
}
body{
  background: #eee;
}
</style>
