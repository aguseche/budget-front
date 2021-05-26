<template>
  <div>
    <HomeHero />
    <About />
  </div>
</template>

<script>
import HomeHero from "@/components/HomeHero.vue";
import About from "@/components/About.vue";
export default {
  name: "Home",
  components: {
    HomeHero,
    About,
  },
  data: () => ({}),
  methods: {},
};
</script>
<style scoped></style>
