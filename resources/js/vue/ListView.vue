<template>
  <div>
    <div v-for="(item, index) in items" :key="index">
      <ListItem :item="item" v-on:itemchanged="$emit('reloadlist')" /> 
    </div>
  </div>
</template>

<script>
import ListItem from "./ListItem";

export default {
  props: ["items"],
  components: {
    ListItem,
  },
};
</script>