<template>
  <v-app>
    <v-container>
      <SearchBlock :searchProp="search" @searchChanged="search = $event"/>
      <FiltersBlock :filtersProp="filters" @filtersChanged="filters = $event"/>
      <div v-if="this.list.length">
        <ContentBlock :list="this.list" :filtersResult="filtersResult"/>
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

    filtersResult() {

        const newArr = this.filters.length > 0 ? [] : this.list

        if (this.filters.length > 0){
          this.filters.forEach(filterObj => {
            this.list.forEach(itemList => {

              const filterNameFormat = filterObj.filterName.toLowerCase()

              if (typeof itemList.ingredients[filterNameFormat] === 'string') {
                itemList.ingredients[filterNameFormat] === filterObj.filterItem && newArr.push(itemList)
              }
              else {
                itemList.ingredients[filterNameFormat].forEach(ingredientsTitle => {
                  ingredientsTitle.name === filterObj.filterItem && newArr.push(itemList)
                })
              }
            })
          })
        }

        if (this.search) {

          return newArr.filter(item => {
                return this.search
                    .toLowerCase()
                    .split(" ")
                    .every(v => item.name.toLowerCase().includes(v));
              }
          )
        }
        else {
          return newArr;
        }
    }
  }
}
</script>
