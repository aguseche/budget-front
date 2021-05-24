<template>
<v-container fluid id="container">
  <!-- Header -->
  <v-row>
    <v-col cols="4" xl="4" lg="4" ></v-col>
    <v-col cols="8" xl="8" lg="8" >
      <header><h1>{{title}}</h1></header>
    </v-col>
  </v-row>
  <v-row class="my-10 py-10">
    <!-- Drop Files -->
    <v-col cols="4" xl="4" lg="4" >
      <v-container class="pl-5 ml-5" style="opacity: .9;">
        <v-card class="pb-5" max-width="300px" max-height="300px">
          <v-card-title><h2 class="py-5 mx-auto">{{filestext}}</h2></v-card-title>
          <v-card-subtitle>
          <!-- File input -->
            <div>
              <label style="cursor: pointer;"
                >
                <v-icon class="circle-icon">mdi-plus</v-icon>
                <input type="file" id="file" ref="file" />
              </label>
            </div>
          </v-card-subtitle>
          <v-card-text>
            <p v-if="file">
            {{file.name}}
            </p>
          </v-card-text>
              <v-btn v-on:click="submitFile()" class="py-3">Submit</v-btn>
        </v-card>
      </v-container>
    </v-col>
    <!-- Paragraph -->
    <v-col cols="8" xl="8" lg="8">
        <v-container id="paragraph-box">
            <p>
                {{paragraph}}
                <br> 
                {{paragraph2}}
                <br> 
                {{paragraph3}}
            </p> 
        </v-container>
        <!-- Button -->
        <v-container id="knowus-box" class="my-10">
          <router-link to="/about"
            style="text-decoration: none; color: inherit;"
          >
            <p class="pb-0 mb-0">{{knowustext}}</p>
          </router-link>
        </v-container>
    </v-col>
  </v-row>
</v-container>
</template>

<script>
import Api from "@/services/api.js";

export default {
  name: "Home",
  components: {},
    data: () => ({
    title: "Budget Management",
    paragraph: "Here you can generate a report",
    paragraph2: "of your expenses based on",
    paragraph3: "a chosen WhatsApp chat",
    filestext: "Add your files",
    knowustext: "Take a look"
  }),
    methods: {
    submitFile() {
      this.file = this.$refs.file.files[0];
      let formData = new FormData();
      formData.append("file", this.file, this.file.name);
      //console.log(this.file);
      Api()
        .post("/monthly-budget", formData)
        .then(response => {
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
    }
  }
};
</script>
<style scoped>
#container {
  background: url("../../public/img/home-image.png") no-repeat center center
    fixed;
  background-size: cover;
  height: 100%;
  width: 100%;
}
header{
  font-size: 40px;
  padding-top:50px;
  margin-top: 50px;
}
h1, h2{
  font-weight: normal;
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
#paragraph-box{
  font-size: 40px;
  max-width: 900px;
}
#knowus-box{
font-size: 25px;
max-width: 300px;
border: 1px solid white;
}

.onhover{
  background-color: white;
  color: black;
  opacity: .9;
}

input[type="file"] {
    display: none;
}
</style>
