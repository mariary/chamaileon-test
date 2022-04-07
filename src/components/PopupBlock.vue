<template>
  <v-container >
    <div>
      <p class="text-h6">{{item.name}}</p>
      <v-img
          :lazy-src="item.image_url"
          height="260"
          width="140"
          :src="item.image_url"
          contain
      ></v-img>
      {{item.description}}
      <div v-for="(type,i) of Object.keys(item.ingredients)" :key="i">
        <span class="font-weight-bold">{{type}}: </span>
        <span v-if="typeof item.ingredients[type] === 'string'">
          {{item.ingredients[type]}}
        </span>
        <span v-else>
          <span v-for="(meal,i) in item.ingredients[type]" :key="i">
            <span>{{meal.name}}</span>
            <span v-if="i !== item.ingredients[type].length - 1">, </span>
          </span>
        </span>
      </div>
    </div>
  </v-container>
</template>

<script>

export default {
    name: 'PopupBlock',

    props: {
      item: Object,
    },

    data: () => ({

    }),

    mounted() {
      for (let kek of Object.keys(this.item.ingredients)) {

        console.log(kek, this.item.ingredients[kek].length);
      }
    }
}
</script>
