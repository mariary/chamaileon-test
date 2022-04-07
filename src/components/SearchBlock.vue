<template>
    <v-col
        cols="12"
        sm="6"
        md="4"
    >
      <v-text-field
          label="Title"
          placeholder="Write beer title..."
          variant="plain"
          :value="searchProp"
          @input="handleSearch"
      ></v-text-field>
    </v-col>
</template>

<script>
  export default {
    name: 'SearchBlock',

    data: () => ({
      searchText: ''
    }),

    props: {
      list: Object,
      searchProp: String
    },

    methods: {
      handleSearch(e) {
        this.searchText = e
        this.$emit('searchChanged', this.searchText)
      }
    }
  }
</script>
