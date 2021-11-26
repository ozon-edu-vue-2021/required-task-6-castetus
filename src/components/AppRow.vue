<template>
  <tr>
    <td>{{row.postId}}</td>
    <td>{{row.id}}</td>
    <td>{{row.name}}</td>
    <td>{{row.email}}</td>
    <td>{{row.body}}</td>
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