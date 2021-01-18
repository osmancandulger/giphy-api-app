<template>
  <div class="gifs">
    <ul>
      <li v-for="item in gifs" :key="item">
        <a :href="item.embed_url" target="_blank">
          <img :src="item.images.fixed_height.url"
        /></a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["gifs"],
};
</script>

<style>
.gifs {
  display: flex;
  justify-content: center;
}
ul {
  display: flex;
  width: 100%;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-top: 75px;
}
li {
  list-style: none;
  transition: 0.4s all;
}
li:hover {
  transform: scale(1.1);
}
</style>
