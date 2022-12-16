<template>
  <div id="app">
    <MainViewPort></MainViewPort>
    <EditViewPortModal></EditViewPortModal>
  </div>
</template>

<script>
import MainViewPort from "./components/MainViewPort.vue";
import EditViewPortModal from "./components/EditViewPortModal.vue";

export default {
  name: "App",
  components: {
    MainViewPort,
    EditViewPortModal,
  },
  mounted() {
    //this.$bvModal.show("edit-view-modal");
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
  min-height: 100vh;
}
</style>
