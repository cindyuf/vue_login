<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #1a202c;
  background: #fdf2f8;
  min-height: 100vh;
  padding: 0;
  margin: 0;
}

body {
  margin: 0;
  padding: 0;
}
</style>