<template>
  <thead>
    <th v-for="title in titles" :key="title" @click="$emit('sort', title)">{{title}}</th>
  </thead>
</template>

<script>
export default {
  name: 'AppTableHeader',
  emits: [
    'sort',
  ],
  props: {
    titles: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
th{
  color: blue;
  text-decoration: underline;
  cursor: pointer;
}
</style>