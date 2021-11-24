<template>
  <thead>
    <th v-for="title in titles" :key="title">{{title}}</th>
  </thead>
</template>

<script>
export default {
  name: 'AppTableHeader',
  props: {
    titles: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style>

</style>