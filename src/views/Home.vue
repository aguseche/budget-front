<template>
  <div>
    <!-- <Toolbar /> -->
    <HomeHero />
    <About />
  </div>
</template>

<script>
import HomeHero from "@/components/HomeHero.vue";
import About from "@/components/About.vue";
// import Toolbar from "@/components/Toolbar.vue";
export default {
  name: "Home",
  components: {
    HomeHero,
    About,
    // Toolbar,
  },
  data: () => ({}),
  methods: {},
};
</script>
<style scoped></style>
