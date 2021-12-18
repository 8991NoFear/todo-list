<template>
  <div>
    <input type="checkbox" @change="updateCheck" v-model="item.completed" />
    <span :class="[item.completed ? 'completed' : '', 'default']">
      {{ item.name }}
    </span>
    <button @click.prevent="removeItem">
      <font-awesome-icon icon="trash" class="trash" />
    </button>
  </div>
</template>

<script>
export default {
  props: ["item"],
  data() {
    return {};
  },
  methods: {
    updateCheck() {
      axios
        .put("/api/item/" + this.item.id)
        .then((response) => {
          if (response.status == 200) {
            this.$emit("itemchanged");
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
    removeItem() {
      axios
        .delete("/api/item/" + this.item.id)
        .then((response) => {
          if (response.status == 200) {
            this.$emit("itemchanged");
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: #999;
}

.default {
  color: black;
}

.trash {
  color: red;
}
</style>