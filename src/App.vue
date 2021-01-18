<template>
  <search></search>
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
      gifs: [],
    };
  },
  created() {
    fetch("http://api.giphy.com/v1/stickers/trending?api_key=dc6zaTOxFJmzC")
      .then((response) => response.json())
      .then((response) => (this.gifs = response.data));
  },
};
</script>

<style>
#app {
  font-family: Roboto, Avenir, Helvetica, Arial, sans-serif;
}
</style>
