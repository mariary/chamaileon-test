<template>
    <v-row
        justify="space-between"
        align="start"
        cols="12"
        sm="6"
        md="3"
    >
      <div
          v-for="(filterName, i) in filtersData"
          :key="i*Math.random()"
          style="padding: 0 20px"
      >
        {{ filterName.label }}
        <v-checkbox
            v-for="(filterItem, i) in filtersData[i].list"
            :key="i*Math.random()"
            :label="filterItem"
            color="orange"
            hide-details
            @change="(e) => handleChooseFilters(e,{filterName: filterName.label, filterItem: filterItem})"
            v-on:input="console.log($event)"
        ></v-checkbox>
      </div>
    </v-row>
</template>

<script>
  export default {
    name: 'FiltersBlock',

    data: () => ({
      filtersData: [
        {
          label: 'Hops',
          list: ['Magnum','Hersbrucker', 'Saaz']
        },
        {
          label: 'Malt',
          list: ['Extra Pale','Munich', 'Caramalt']
        },
        {
          label: 'Yeast',
          list: ['Wyeast 2007 - Pilsen Lager','Wyeast 1056 - American Ale', 'Wyeast 3711 - French Saison']
        },
      ],
      filters: [],
    }),

    props: {
      filtersProp: Array,
    },

    methods: {
      handleChooseFilters(checked, obj) {
        if (checked) {
          this.filters.push(obj)
        }
        else {
          this.filters = this.filters.filter(x => x.filterItem !== obj.filterItem)
        }
        this.$emit('filtersChanged', this.filters)
      }
    }
  }
</script>
