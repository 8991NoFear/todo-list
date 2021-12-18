<template>
  <div class="todo-list-container">
    <div class="heading">
      <h2 id="title">Todo List</h2>
      <AddItemForm v-on:reloadlist="getList" />
    </div>
    <ListView :items="items" v-on:reloadlist="getList" />
  </div>
</template>

<script>
import ListView from "./ListView";
import AddItemForm from "./AddItemForm";

export default {
  components: {
    ListView,
    AddItemForm,
  },
  data() {
    return {
      items: [],
    };
  },
  methods: {
    getList() {
      axios
        .get("/api/items")
        .then((response) => {
          this.items = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  created() {
    this.getList();
  },
};
</script>