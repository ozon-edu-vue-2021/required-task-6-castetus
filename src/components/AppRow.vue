<template>
  <tr>
    <td>{{row.id}}</td>
    <td>{{row.name}}</td>
    <td>{{row.body}}</td>
    <td>{{row.email}}</td>
  </tr>
</template>

<script>
export default {
  name: 'AppRow',
  props: {
    row: {
      type: Object,
      default: () => {},
    },
  },
}
</script>

<style scoped>
  tr td {
    border: 1px solid grey;
  }
</style>