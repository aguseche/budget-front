<template>
  <v-container id="header" fluid class="home-hero">
    <!-- Header -->
    <v-row>
      <v-col cols="4" xl="4" lg="4" md="4" class="hidden-sm-and-down"></v-col>
      <v-col cols="12" xl="8" lg="8" md="8" sm="12" xs="12">
        <header>
          <h1>{{ title }}</h1>
        </header>
      </v-col>
    </v-row>
    <v-row class="my-10 py-10">
      <!-- Drop Files -->
      <v-col cols="4" xl="4" lg="4" md="4" sm="12" xs="12">
        <v-container class="pl-5 ml-5" style="opacity: 0.9">
          <v-card class="pb-5" max-width="300px" max-height="300px">
            <v-card-title
              ><h2 class="py-5 mx-auto">{{ filestext }}</h2></v-card-title
            >
            <v-card-subtitle>
              <!-- File input -->
              <div>
                <label style="cursor: pointer">
                  <v-icon class="circle-icon">mdi-plus</v-icon>
                  <input
                    type="file"
                    id="file"
                    ref="file"
                    accept=".csv, text/plain"
                    @change="fileChanged"
                  />
                </label>
              </div>
            </v-card-subtitle>
            <v-card-text>
              <!-- Show files name (does not work) -->
              <p v-if="filename" class="pb-0 mb-0">
                {{ filename }}
              </p>
            </v-card-text>
            <v-btn v-on:click="submitFile()" class="py-3">Submit</v-btn>
          </v-card>
        </v-container>
      </v-col>
      <!-- Paragraph -->
      <v-col cols="12" xl="8" lg="8" md="8" sm="12" xs="12">
        <v-container id="paragraph-box">
          <p>
            {{ paragraph }}
            <br />
            {{ paragraph2 }}
            <br />
            {{ paragraph3 }}
          </p>
        </v-container>
        <!-- Button -->
        <a href="#text">
          <v-container id="knowus-box" class="my-10">
            {{ knowustext }}
          </v-container>
        </a>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Api from "@/services/api.js";

export default {
  name: "HomeHero",
  components: {},
  data: () => ({
    title: "Budget Management",
    paragraph: "Here you can generate a report",
    paragraph2: "of your expenses based on",
    paragraph3: "a chosen WhatsApp chat",
    filestext: "Add your files",
    knowustext: "Take a look",
    filename: "",
  }),
  methods: {
    submitFile() {
      this.file = this.$refs.file.files[0];
      let formData = new FormData();
      formData.append("file", this.file, this.file.name);
      //console.log(this.file);
      Api()
        .post("/monthly-budget", formData)
        .then((response) => {
          console.log(response);
          const downloadUrl = window.URL.createObjectURL(
            new Blob([response.data])
          );
          this.invoicePDF = downloadUrl;
          this.downloadFile();
        });
    },
    downloadFile() {
      const link = document.createElement("a");
      link.href = this.invoicePDF;
      link.setAttribute("download", "budget_report.pdf");
      document.body.appendChild(link);
      link.click();
      link.remove();
    },
    fileChanged(e) {
      this.filename = e.target.files[0].name;
    },
  },
};
</script>
<style scoped>
.home-hero {
  background: url("../../public/img/home-image.png") no-repeat center center;
  background-size: cover;
  height: 100%;
  width: 100%;
  min-height: 100vh;
}
header {
  font-size: 40px;
  padding-top: 50px;
  margin-top: 50px;
}
.circle-icon {
  background: #8da6ca;
  width: 75px;
  height: 75px;
  border-radius: 50%;
  text-align: center;
  line-height: 100px;
  vertical-align: middle;
  padding: 30px;
}
#paragraph-box {
  font-size: 40px;
  max-width: 900px;
}
a {
  text-decoration: none;
  color: white !important;
}
#knowus-box {
  font-size: 25px;
  max-width: 300px;
  border: 1px solid white;
}
#knowus-box:hover {
  background-color: white;
  color: black;
  opacity: 0.9;
}
input[type="file"] {
  display: none;
}
</style>
