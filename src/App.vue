<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: url('https://wallpaperaccess.com/full/1289919.jpg');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}
html, body, #app {
  height: 100%;
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  overflow: hidden;

}
</style>
