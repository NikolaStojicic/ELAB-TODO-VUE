<template>
  <div>
    <b-container class="bv-example-row">
      <b-row>
        <b-col xs="12" sm="6" md="4" v-for="list in lists" :key="list.id">
          <b-badge @click.prevent="deleteList(list)" id="listclose" href="#" variant="danger" pill>X</b-badge>
          <b-card-group deck>
            <b-card class="mt-5 mx-1" no-body :header="list.title">
              <b-list-group flush>
                <ListItem @update-lists="updateUi" @delete-item="deleteItem" :list="list" />
              </b-list-group>
            </b-card>
          </b-card-group>
        </b-col>
        <b-col xs="12" sm="6" md="4">
          <b-card-group deck>
            <b-card class="mt-5 mx-1" no-body>
              <b-input-group prepend="New list">
                <b-form-input v-model="newListTitle"></b-form-input>
                <b-input-group-append>
                  <b-button @click="addList" size="sm" text="Add" variant="success">Add</b-button>
                </b-input-group-append>
              </b-input-group>
            </b-card>
          </b-card-group>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import ListItem from "@/components/ListItem.vue";
export default {
  components: {
    ListItem
  },

  methods: {
    async updateUi() {
      const response = await this.$http.get(
        `${this.$store.state.baseUrl}/liste.json`
      );
      this.lists = response.data;
    },
    async deleteList(list) {
      await this.$http.delete(`${this.$store.state.baseUrl}/liste/${list.id}`);
      this.updateUi();
    },

    async addList() {
      if (this.newListTitle.length < 1) return;
      await this.$http.post(`${this.$store.state.baseUrl}/liste`, {
        title: this.newListTitle
      });
      this.newListTitle = "";
      this.updateUi();
    }
  },
  async mounted() {
    this.updateUi();
  },
  data() {
    return {
      lists: [],
      newListTitle: ""
    };
  }
};
</script>

<style lang="scss" scoped>
#listclose {
  position: absolute;
  top: 40px;
  right: 0px;
  z-index: 1;
}
@media (max-width: 576px) {
  #listclose {
    right: 5px;
  }
}
</style>