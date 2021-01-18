<template>
  <search v-on:requested="searchButton"></search>
  <div class="loader-container">
    <div class="loader" v-if="loading"></div>
  </div>
  <h1 class="error" v-if="gifs.length == 0 && !loading">
    We couldn't find your GIF
  </h1>
  <overview :gifs="gifs"></overview>
</template>
<script>
import Search from "./components/Search.vue";
import Overview from "./components/Overview.vue";
export default {
  name: "App",
  components: {
    Search,
    Overview,
  },
  data() {
    return {
      api_key: process.env.VUE_APP_API_SECRET_KEY,
      loading: true,
      gifs: [],
    };
  },
  methods: {
    searchButton(search) {
      this.gifs = [];
      this.loading = true;
      fetch(
        `http://api.giphy.com/v1/gifs/search?q=${search}&api_key=${this.api_key}`
      )
        .then((response) => response.json())
        .then((response) => {
          this.gifs = response.data;
          this.loading = false;
        });
    },
  },
  created() {
    fetch(`http://api.giphy.com/v1/gifs/trending?api_key=${this.api_key}`)
      .then((response) => response.json())
      .then((response) => {
        this.gifs = response.data;
        this.loading = false;
      });
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,900;1,100&display=swap");
#app {
  font-family: "Roboto", sans-serif;
}
.loader-container {
  display: flex;
  width: 100%;
  justify-content: center;
  position: relative;
  top: 45px;
}
.loader {
  width: 120px;
  height: 120px;
  border: 15px solid #f3f3f3;
  border-radius: 50%;
  border-top: 15px solid #3498db;
  border-right: 15px solid green;
  animation: spin 0.4s linear infinite;
}
/* Safari */
@-webkit-keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
.error {
  display: flex;
  position: relative;
  justify-content: center;
  align-items: center;
  bottom: 35px;
  height: 250px;
  font-weight: 900;
}
</style>
