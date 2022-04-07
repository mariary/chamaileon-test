<template>
  <v-row class="wrapper">
   <ItemBeer
        :item="item"
        v-for="(item) in filterResult"
        :key="item.id"
   />
  </v-row>
</template>

<script>

import ItemBeer from "@/components/ItemBeer";
export default {
    name: 'ContentBlock',
    components: {ItemBeer},
    props: {
      list: Array,
      searchResult: Array,
      filterResult: Array
    },

    data: () => ({

    }),
}
</script>

<style>
.wrapper {
  margin: 20px 0;
}
</style>
