<template>
  <v-container fluid class="information-section">
    <v-row id="user-guide">
      <v-col align="start"
        ><header>
          <h1 class="py-4 my-4 pl-15 ml-15">{{ heading }}</h1>
        </header></v-col
      >
    </v-row>
    <v-container v-for="item in instructions" :key="item.number">
      <v-row class="">
        <v-col align="center">
          <p class="round-item">{{ item.number }}</p>
        </v-col>
        <v-col align="center">
          <p>{{ item.text }}</p>
          <v-row v-if="item.number === 2">
            <v-col>
              Price Type Description(Optional) <br />
              For example: 1000 food supermarket <br />
              or 2000 house april rent
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
    <v-row>
      <!-- Button -->
      <v-col>
        <a href="#header">
          <v-container id="gototop-box" class="my-10">
            I want to try !
          </v-container>
        </a>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name: "About",
  components: {},
  data: () => ({
    heading: "Get started with 5 simple steps",
    instructions: [
      {
        number: 1,
        text: "Create a whatsapp group",
      },
      {
        number: 2,
        text: "Register your expenses sending messages using this format",
      },
      {
        number: 3,
        text: "Export the chat to your computer",
      },
      {
        number: 4,
        text: "Unzip it and add it with the + icon above",
      },
      {
        number: 5,
        text: "Submit and accept the download",
      },
    ],
  }),
};
</script>
<style scoped>
.information-section {
  background-color: #755946;
}
h1 {
  font-size: 50px;
}
.round-item {
  background-color: #463529;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  padding: 5px;
  text-align: center;
}
p {
  font-size: 25px;
}
a {
  text-decoration: none;
  color: white !important;
}
#gototop-box {
  font-size: 25px;
  max-width: 300px;
  border: 1px solid white;
}
#gototop-box:hover {
  background-color: white;
  color: black;
  opacity: 0.9;
}
</style>
