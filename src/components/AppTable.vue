<template>
  <div class="app-table">
    <button>pagination</button>
    <button>Infinite scroll</button>
    <table>
      <thead>
        <tr>
          <AppTableHeaderEl
            v-for="title in titles"
            :key="title"
            :title="title"
            @sort="sortTable"
            @filter="filterTable"/>
        </tr>
      </thead>
      <tbody>
        <AppRow v-for="row in filteredData" :key="row.id" :row="row" />
      </tbody>
    </table>
  </div>
</template>

<script>
import AppRow from './AppRow.vue';
import AppTableHeaderEl from './AppTableHeaderEl.vue';

export default {
  name: 'AppTable',
  components: {
    AppRow,
    AppTableHeaderEl,
  },
  props: {
    rows: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      tableData: [],
      filters: [],
    };
  },
  created() {
    this.tableData = JSON.parse(JSON.stringify(this.rows));
  },
  computed: {
    titles() {
      if (this.rows.length) {
        return Object.keys(this.rows[0]);
      }
      return [];
    },
    filteredData() {
      const filterFunc = (row, filter) => {
        return row[filter.column].toLowerCase().includes(filter.string.toLowerCase());
      }
      if (this.filters.length) {
        return this.tableData.filter((row) => {
          return this.filters.every(filter => filterFunc(row, filter));
        });
      }
      return this.tableData;
    },
  },
  methods: {
    sortTable(params) {
      this.tableData.sort((a, b) => {
        let result = 0;
        const aData = a[params.column];
        const bData = b[params.column];
        if (aData > bData) {
          result = 1;
        } else if (bData > aData) {
          result = -1;
        }
        return result * params.order;
      });
    },
    filterTable(params) {
      const existingFilter = this.filters.find((filter) => filter.column === params.column);
      if (existingFilter) {
        existingFilter.string = params.string;
      } else {
        this.filters.push(params);
      }
    },
  },
};
</script>

<style>

</style>