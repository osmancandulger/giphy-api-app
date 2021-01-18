<template>
  <search v-on:requested="searchButton"></search>
  <div class="loader" v-if="loading"></div>
  <h1 v-if="gifs.length == 0 && !loading">There is no search</h1>

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
#app {
  font-family: Roboto, Avenir, Helvetica, Arial, sans-serif;
}

.loader {
  border: 15px solid #f3f3f3;
  border-radius: 50%;
  border-top: 15px solid #3498db;
  border-right: 15px solid green;
  width: 120px;
  height: 120px;

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
</style>
