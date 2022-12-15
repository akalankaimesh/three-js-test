<template>
  <div id="app">
    <MainViewPort></MainViewPort>
  </div>
</template>

<script>
import MainViewPort from "./components/MainViewPort.vue";

export default {
  name: "App",
  components: {
    MainViewPort,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  padding: 0;
  margin: 0;
}
</style>
