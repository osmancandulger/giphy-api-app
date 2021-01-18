<template>
  <div class="search-bar">
    <input
      placeholder="Put some words in here !"
      onfocus="this.placeholder=''"
      onblur="this.placeholder='Put some words in here !'"
      type="text"
      v-model="search"
      v-on:keypress.enter="searchButton"
    />
    <button @click="searchButton">
      Find My Mood
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: "",
    };
  },
  methods: {
    searchButton() {
      this.$emit("requested", this.search);
    },
  },
};
</script>

<style lang="scss">
.search-bar {
  display: flex;
  width: 100%;
  justify-content: center;
  margin: 35px;
  align-items: center;
  input {
    width: 350px;
    height: 45px;
    border-radius: 15px;
    padding-left: 15px;
    outline: none;
    border: none;
    background: #bfdad3;
  }
  input::placeholder {
    color: rgb(99, 92, 92);
    padding-left: 10px;
    opacity: 0.7;
  }
  button {
    position: relative;
    left: 10px;
    width: 150px;
    height: 45px;
    border: none;
    border-radius: 15px;
    outline: none;
    cursor: pointer;
    transition: 0.4s all;
  }
  button:hover {
    transform: scale(1.06);
    color: #87a2a8;
  }
}
</style>
