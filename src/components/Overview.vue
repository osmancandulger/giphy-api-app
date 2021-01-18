<template>
  <div class="gifs">
    <ul>
      <li v-for="item in gifs" :key="item">
        test
      </li>
    </ul>
  </div>
</template>

<script>
export default {
    props:['gifs']
  data() {
    return {

    };
  },
};
</script>

<style></style>
