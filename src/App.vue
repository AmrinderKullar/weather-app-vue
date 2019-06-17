<template>
  <div id="app">
   <HomeContainer />
  </div>
</template>

<script>
  import HomeContainer from './containers/HomeContainer.vue';

  export default {
    name: "app",
    components: {
      HomeContainer,
    },
  };
</script>

<style>
#app {
  width: 100%;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
