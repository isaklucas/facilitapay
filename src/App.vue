<template>
  <div id="app">
    <Header />
    <router-view />
  </div>
</template>
<script lang="ts">
import Vue from "vue";
import Header from "./components/Header.vue";
export default Vue.extend({
  components: {
    Header,
  },
});
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
}

body {
  background-image: url(assets/background.svg);
  background-size: cover;

  margin: 0;
  padding: 0;
}
</style>
