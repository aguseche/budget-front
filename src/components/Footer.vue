<template>
  <div class="">
    <v-footer padless class="">
      <v-container fluid class="footer">
        &copy;
        {{ currentYear }}
        -
        {{ productedby }}
      </v-container>
    </v-footer>
  </div>
</template>

<script>
export default {
  data: () => ({
    items: [
      {
        icon: "mdi-whatsapp",
        url: "#",
      },
      {
        icon: "mdi-twitter",
        url: "#",
      },
      {
        icon: "mdi-linkedin",
        url: "#",
      },
      {
        icon: "mdi-instagram",
        url: "#",
      },
    ],
    productedby: "Agustin Etcheverry",
  }),
  computed: {
    currentYear() {
      return new Date().getFullYear();
    },
  },
};
</script>
<style>
a {
  text-decoration: none;
}
.footer {
  background-color: #463529;
  color: white;
}
</style>
