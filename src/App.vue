<template>
  <div id="app">
    <Home />
  </div>
</template>

<script>
import Home from "./components/Home";
export default {
  name: "App",
  components: {
    Home,
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap");
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
  background-color: #ecf1f6;
}
#app {
  padding: 20px;
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
  @media (max-width: $TableWidth) {
    padding: 20px 5px;
  }
}
h2 {
  margin: 0;
}
ul {
  padding: 0;
  margin: 0;
  list-style: none;
}
p {
  margin: 0;
}
</style>
