<template>
  <th>
    <span @click="sortColumn">{{title}}</span>
    <ArrowDown v-if="order === 1"/>
    <ArrowUp v-if="order === -1"/>
    <input
      type="text"
      placeholder="filter"
      v-model="filterString"
      @input="filter">
  </th>
</template>

<script>
import ArrowDown from 'vue-material-design-icons/ArrowDown.vue';
import ArrowUp from 'vue-material-design-icons/ArrowUp.vue';


export default {
  name: 'AppTableHeaderEl',
  emits: [
    'sort',
    'filter',
  ],
  components: {
    ArrowDown,
    ArrowUp,
  },
  props: {
    title: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      order: 0,
      filterString: '',
    };
  },
  methods: {
    sortColumn() {
      if (!this.order) {
        this.order = 1;
      } else {
        this.order = this.order * -1;
      }
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