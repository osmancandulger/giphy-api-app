<template>
  <div class="search-bar">
    <input type="text" placeholder="Put some words in here !" />
    <button>Find My Mood</button>
  </div>
</template>

<script>
export default {};
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
    
  }
}
</style>
