<template>
  <div id="app">
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      rows: [],
    };
  },
  async created() {
    const res = await fetch(`https://jsonplaceholder.typicode.com/comments`);
    this.rows = await res.json();
  }
};
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>