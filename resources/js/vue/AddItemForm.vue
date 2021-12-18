<template>
  <div class="add-item-form">
    <input type="text" v-model="item.name" />
    <font-awesome-icon
      icon="plus-square"
      :class="[item.name ? 'active' : 'inactive', 'default']"
      @click="addItem"
    />
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      item: {
        name: "",
      },
    };
  },
  methods: {
    addItem() {
      if (this.item == "") {
        return;
      }
      
      axios
        .post("/api/item/store", {
          item: this.item,
        })
        .then((response) => {
          if (response.status == 201) {
            this.item.name = "";
            this.$emit('reloadlist');
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
.default {
}

.active {
  color: #fabfab;
}

.inactive {
  color: #aaa;
}
</style>