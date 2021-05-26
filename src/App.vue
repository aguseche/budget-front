<template>
  <v-app id="app">
    <v-main>
      <router-view />
    </v-main>
    <Footer />
  </v-app>
</template>

<script>
import Footer from "./components/Footer";

export default {
  name: "App",

  data: () => ({
    //
  }),
  components: {
    Footer,
  },
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Libre+Baskerville&display=swap");
#app {
  font-family: "Libre Baskerville", Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
}
h1,
h2 {
  font-weight: normal;
}
</style>
