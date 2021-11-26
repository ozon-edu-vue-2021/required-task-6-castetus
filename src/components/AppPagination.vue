<template>
  <div class="app-pagination">
    <button
      v-for="page in pages"
      :key="page"
      :class="{active: currentPage === page}"
      @click="changePage(page)">
      {{page + 1}}
    </button>
  </div>
</template>

<script>
export default {
  name: 'AppPagination',
  props: {
    pages: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      currentPage: 0,
    };
  },
  methods: {
    changePage(page) {
      this.$emit('changePage', page);
      this.currentPage = page;
    }
  }
};
</script>

<style scoped>
  .active{
    background: green;
  }
</style>