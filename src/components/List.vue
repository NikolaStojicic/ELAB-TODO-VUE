<template>
  <div>
    <b-list-group>
      <b-list-group-item
        v-for="(item, id) in items"
        :key="id"
        class="d-flex justify-content-between align-items-center"
        variant="primary"
      >
        item
        <b-badge href="#" variant="danger" pill>X</b-badge>
      </b-list-group-item>
    </b-list-group>
  </div>
</template>

<script>
export default {
  mounted() {},
  data() {
    return {
      items: [
        {
          variant: "primary",
          content: "Primary list group"
        },
        {
          variant: "primary",
          content: "Primary list group"
        },
        {
          variant: "primary",
          content: "Primary list group"
        },
        {
          variant: "primary",
          content: "Primary list group"
        }
      ]
    };
  }
};
</script>

<style lang="scss" scoped>
</style>