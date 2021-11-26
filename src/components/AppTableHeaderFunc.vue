<script lang="jsx">
export default {
  name: 'AppTableHeader',
  functional: true,
  emits: [
    'sort',
  ],
  props: {
    titles: {
      type: Array,
      default: () => [],
    },
  },
  render: function(h, ctx) {
    const titles = ctx.props.title;
    return titles.map((title) => {
      <th key={title} nativeOnClick={$emit('sort', title)}>{title}</th>
    });
  }
};
</script>

<style scoped>
th{
  color: blue;
  text-decoration: underline;
  cursor: pointer;
}
</style>