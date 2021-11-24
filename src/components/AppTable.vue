<template>
  <table>
    <AppTableHeader :titles="titles" />
    <tbody>
      <AppRow v-for="row in rows" :key="row.id" :row="row" />
    </tbody>
  </table>
</template>

<script>
import AppRow from './AppRow.vue';
import AppTableHeader from './AppTableHeader.vue';

export default {
  name: 'AppTable',
  components: {
    AppRow,
    AppTableHeader,
  },
  props: {
    rows: {
      type: Array,
      default: () => [],
    },
  },
  computed: {
    titles() {
      return Object.keys(this.rows[0]);
    },
  },
};
</script>

<style>

</style>