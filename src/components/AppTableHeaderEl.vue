<template>
  <th>
    <span @click="sortColumn">{{title}}</span>
    <input
      type="text"
      placeholder="filter"
      v-model="filterString"
      @input="filter">
  </th>
</template>

<script>
export default {
  name: 'AppTableHeaderEl',
  emits: [
    'sort',
    'filter',
  ],
  props: {
    title: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      order: -1,
      filterString: '',
    };
  },
  methods: {
    sortColumn() {
      this.order = this.order * -1;
      this.$emit('sort', {
        column: this.title,
        order: this.order,
      });
    },
    filter() {
      this.$emit('filter', {
        column: this.title,
        string: this.filterString,
      });
    },
  },
}
</script>

<style scoped>
th{
  color: blue;
  text-decoration: underline;
  cursor: pointer;
}
</style>