<template>
  <span @click.stop>
    <b-badge @click="enabled = !enabled" class="mt-2" href="#" variant="info" pill>Edit</b-badge>
    <div id="form" v-if="enabled">
      <b-form-group>
        <b-form-input v-model="content" size="sm" :placeholder="label"></b-form-input>
      </b-form-group>
      <b-row class="justify-content-around">
        <b-col>
          <b-button @click="enabled = !enabled" block variant="danger" size="sm">Exit</b-button>
        </b-col>
        <b-col>
          <b-button @click="changeTitle" block variant="info" size="sm">Change</b-button>
        </b-col>
      </b-row>
    </div>
  </span>
</template>

<script>
export default {
  props: {
    label: {
      type: String
    }
  },
  methods: {
    changeTitle() {
      if (this.content.length < 1) return;
      this.$emit("changeItem", this.content);
      this.content = "";
      this.enabled = false;
    }
  },
  data() {
    return {
      enabled: false,
      content: ""
    };
  }
};
</script>

<style scoped>
#form {
  width: 200px;
  background-color: rgb(240, 240, 240);
  position: absolute;
  z-index: 2;
  border-radius: 5px;
  padding: 5px;
}
</style>