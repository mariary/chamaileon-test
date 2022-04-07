<template>
  <v-app>
    <v-container>
      <SearchBlock :searchProp="search" @searchChanged="search = $event"/>
      <FiltersBlock :filtersProp="filters" @filtersChanged="filters = $event"/>
      <div v-if="this.list.length">
        <ContentBlock :list="this.list" :searchResult="searchResult" :filterResult="filtersResult"/>
      </div>
    </v-container>
  </v-app>
</template>

<script>
import SearchBlock from "@/components/SearchBlock";
import FiltersBlock from "@/components/FiltersBlock";
import ContentBlock from "@/components/ContentBlock";

export default {
  name: 'App',

  components: {
    ContentBlock,
    SearchBlock,
    FiltersBlock
  },

  data: () => ({
    apiUrl: 'https://api.punkapi.com/v2/beers',
    list: [],
    search: '',
    filters: [],
  }),

  mounted() {
    this.fetchUserData()
  },

  methods: {
    async fetchUserData() {
      try {
        const response = await fetch(this.apiUrl)
        const res = await response.json()
        this.list = res
      }
      catch (e) {
        console.log(e);
      }
    }
  },
  computed: {
    searchResult() {
      console.log(this.filters);
      if (this.search) {
        return this.list.filter(item => {
              return this.search
                  .toLowerCase()
                  .split(" ")
                  .every(v => item.name.toLowerCase().includes(v));
            }
        );
      }
      else {
        return this.list;
      }
    },

    filtersResult() {
      if (this.filters.length) {
        let result = this.list
        console.log(result)
        
        for (let i = 0; i < this.filters.length; i++){
          let kek = this.filters[i]
          result = this.list.map(
              x => x.ingredients[kek.filterName]
              .filter(y => y.name === kek.filterItem.toLowerCase()))
              .filter(x => x.length > 0)
        }
        console.log(result)
            /*.map(filter => {
              this.list = this.list.filter(itemList => itemList.filterName.toLowerCase() )
                /!*.filter(itemList => {
                  const name = filter.filterName.toLowerCase()
                  return itemList.ingredients[name] === 'string'*!/
                /!*  return typeof itemList.ingredients[name] === 'string'
                      ? itemList.ingredients[name] === filter.filterItem
                      : itemList.map(x => x.ingredients[filter.filterName].filter(y => y.name == filter.filterItem)).filter(x => x.length > 0)
                *!/})
            })*/
      }
      return this.list;
    },
  },
};
</script>
