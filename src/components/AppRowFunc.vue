<script lang="jsx">
export default {
  name: 'AppRow',
  functional: true,
  props: {
    row: {
      type: Object,
      default: () => {},
    },
  },
  render: function(h, ctx) {
    const { postId, id, name, email, body } = ctx.props.row;
    return (
        <tr>
          <td>{postId}</td>
          <td>{id}</td>
          <td>{name}</td>
          <td>{email}</td>
          <td>{body}</td>
        </tr>
    );
  },
}
</script>

<style scoped>
  tr td {
    border: 1px solid grey;
  }
</style>