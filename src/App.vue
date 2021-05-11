<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/peiko-logo-mini.png" />
    <h1>Test</h1>
    <MainTable />
    <hr />
  </div>
</template>

<script>
import MainTable from "./components/table/MainTable";
export default {
  name: "App",
  components: {
    MainTable,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
