<template>
  <div class="list">
    <Item :key="item.id" v-for="item in items" :item="item" />
  </div>
</template>

<script>
import Item from "../item/item.vue"
export default {
  components: {
    Item,
  },
  name: 'list',
  props: {
    items: Array
  }
}
</script>
