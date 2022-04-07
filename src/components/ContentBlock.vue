<template>
  <v-row class="wrapper">
   <ItemBeer
        :item="item"
        v-for="(item) in filtersResult"
        :key="item.id*Math.random()"
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
      filtersResult: Array,
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
