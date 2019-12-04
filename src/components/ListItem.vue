<template>
  <div>
    <b-list-group-item
      href="#"
      @click="changeStatus(item)"
      v-for="(item, id) in list.itemi"
      :key="id"
      class="d-flex justify-content-between align-items-center"
      :variant="(item.status == '0')?'primary':'success'"
    >
      <div
        :style="(item.status == '0')?'textDecoration: none;':'textDecoration: line-through'"
      >{{id + 1}}. {{item.content}}</div>
      <b-badge @click.stop="deleteItem(item)" href="#" variant="danger" pill>X</b-badge>
    </b-list-group-item>

    <b-input-group class="mt-1" prepend="New item">
      <b-form-input v-model="newItem"></b-form-input>
      <b-input-group-append>
        <b-button @click="addItem(list)" size="sm" text="Add" variant="success">Add</b-button>
      </b-input-group-append>
    </b-input-group>
  </div>
</template>

<script>
export default {
  props: {
    list: {
      type: Object
    }
  },
  data() {
    return {
      newItem: ""
    };
  },
  methods: {
    async deleteItem(item) {
      await this.$http.delete(`${this.$store.state.baseUrl}/itemi/${item.id}`);
      this.$emit("update-lists");
    },
    async changeStatus(item) {
      const resBody = {
        status: item.status == "0" ? "1" : "0",
        content: item.content,
        list_id: item.list_id
      };
      await this.$http.put(
        `${this.$store.state.baseUrl}/itemi/${item.id}`,
        resBody
      );
      this.$emit("update-lists");
    },
    async addItem(list) {
      const resBody = { content: this.newItem, status: 0, list_id: list.id };
      await this.$http.post(`${this.$store.state.baseUrl}/itemi`, resBody);
      this.newItem = "";
      this.$emit("update-lists");
    }
  }
};
</script>

<style lang="scss" scoped>
</style>