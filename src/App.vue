<template>
  <div id="app">
    <trade />
  </div>
</template>

<script>
import trade from "./components/paymentbutton";

export default {
  name: "App",
  components: {
    trade,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
