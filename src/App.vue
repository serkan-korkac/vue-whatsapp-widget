<template>
  <div id="app">
    <Widget phoneNumber="+11111111111" />
  </div>
</template>

<script>
import Widget from "./components/Widget.vue";

export default {
  name: "WhastAppWidget",
  components: {
    Widget,
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
</style>
