<template>
  <div id="app">
    <Header />
    <Layout />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Layout from "./components/Layout.vue";

export default {
  name: "App",
  components: {
    Header,
    Layout,
  },
};
</script>

<style>
body {
  background-color: #16191c !important;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.sr-only {
  display: none;
}
thead {
  border-bottom: 5px solid #16191c !important;
}
</style>
