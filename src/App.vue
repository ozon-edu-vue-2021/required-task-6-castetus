<template>
  <div id="app">
    <AppTable :rows="rows" />
  </div>
</template>

<script>
import AppTable from './components/AppTable.vue';

export default {
  name: 'App',
  components: {
    AppTable,
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