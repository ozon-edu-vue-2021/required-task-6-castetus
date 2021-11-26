<template>
  <div class="app-table">
    <div class="actions">
      <label for="numberPosts">Show by: </label>
      <select
        name="numberPosts"
        v-model="numberPosts"
        @change="paginate()">
        <option
          v-for="option in options"
          :key="option.num"
          :value="option.num">
          {{option.title}}
        </option>
      </select>
      <AppPagination
        v-if="numberPosts"
        :pages="pages"
        @changePage="changePage"/>
      <!-- <button>Infinite scroll</button> -->
    </div>
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
        <AppRow v-for="row in paginatedData" :key="row.id" :row="row" />
      </tbody>
    </table>
  </div>
</template>

<script>
import AppRow from './AppRow.vue';
import AppTableHeaderEl from './AppTableHeaderEl.vue';
import AppPagination from './AppPagination.vue';

export default {
  name: 'AppTable',
  components: {
    AppRow,
    AppTableHeaderEl,
    AppPagination,
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
      numberPosts: 0,
      // pagination: false,
      options: [
        {
          num: 50,
          title: '50 posts per page',
        },
        {
          num: 100,
          title: '100 posts per page',
        },
        {
          num: 0,
          title: 'All posts',
        },
      ],
      currentPage: 0,
      pages: [],
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
    paginatedData() {
      if (!!this.numberPosts) {
        const beginIndex = this.numberPosts * this.currentPage;
        const endIndex = beginIndex + this.numberPosts;
        return this.filteredData.slice(beginIndex, endIndex);
      }
      return this.filteredData;
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
    paginate() {
      const pages = [];
      if (this.numberPosts) {
        const numberPages = this.rows.length / this.numberPosts;
          for (let i = 0; i < numberPages; i++) {
            pages.push(i);
          }
        }
      this.pages = pages;
    },
    changePage(page) {
      this.currentPage = page;
      console.log(page);
    },
  },
};
</script>

<style>
button {
  border: none;
  background: blue;
  color: white;
  border-radius: 5px;
  padding: 10px 20px;
  margin: 10px;
  cursor: pointer;
}
select {
  height: 20px;
}
.actions{
  display: flex;
  width: 100%;
}
</style>