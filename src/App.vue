<template>
  <p v-if="loading">Loading..</p>
  <search @requested="searchButton"></search>
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
      loading: true,
      gifs: [],
    };
  },
  methods: {
    searchButton(search) {
      this.gifs = [];
      this.loading = true;
      fetch(`http://api.giphy.com/v1/gifs/search?q=${search}&api_key=dc6zaTOxFJmzC`)
        .then((response) => response.json())
        .then((response) => {
          this.gifs = response.data;
          this.loading = false;
        });
    },
  },
  created() {
    fetch("http://api.giphy.com/v1/gifs/trending?api_key=dc6zaTOxFJmzC")
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
</style>
