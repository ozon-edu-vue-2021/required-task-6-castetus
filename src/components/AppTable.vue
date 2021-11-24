<template>
  <table>
    <AppRow v-for="row in rows" :key="row.id" :row="row" />
  </table>
</template>

<script>
import AppRow from './AppRow.vue';

export default {
  name: 'AppTable',
  components: {
    AppRow,
  },
  props: {
    rows: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style>

</style>