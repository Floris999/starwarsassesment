<template>
  <div id="app">
    <nav class="menu-list">
      <router-link to="/">Home</router-link>
      <router-link to="/">About this project</router-link>
      <router-link to="/">Contact us</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<script>

  export default {
      name: 'App',
      components: {
      
      }
  }
</script>


<style>
/* Font import */
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;700&display=swap');
body{
  margin: 0px;
  font-family: 'Open Sans', sans-serif;
  min-height: 100vh;
}
h2 {
  color: white;
  font-size: 24px;
}
h3 {
  color: #FFE81F;
  font-size: 14px;
}
ul {
    list-style: none;
    margin: 0px;
}
li {
    margin: 10px 0px;
    font-size: 16px;
}

a {
  color: black;
  text-decoration: none;
}

.menu-list {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  gap: 20px;
  background-color: #FFE81F;
  padding: 20px;
  margin: 0px;
  box-shadow: inset 0 0 10px #000000;
}
@media only screen and (max-width: 1200px) {
  .menu-list {
      justify-content: center;
      width: 100%;
  }
}
</style>
