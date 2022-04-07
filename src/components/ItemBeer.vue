<template>
  <v-col
      cols="12"
      md="4"
  >
      <v-card height="400px">
        <v-card-title class="text-body-1 font-weight-bold">{{item.name}}</v-card-title>
        <v-img
            :lazy-src="item.image_url"
            height="260"
            width="140"
            :src="item.image_url"
            contain
        ></v-img>
        <p class="text">{{decreaseStrLength(item.description)}}</p>
      </v-card>
    <v-col cols="auto" align="center">
      <v-dialog
          transition="dialog-top-transition"
          max-width="600"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
              color="primary"
              v-bind="attrs"
              v-on="on"
          >Show more</v-btn>
        </template>
        <template v-slot:default="dialog">
          <v-card>
            <PopupBlock :item="item"/>
            <v-card-actions class="justify-end">
              <v-btn
                  text
                  @click="dialog.value = false"
              >Close</v-btn>
            </v-card-actions>
          </v-card>
        </template>
      </v-dialog>
    </v-col>
  </v-col>
</template>

<script>
  import PopupBlock from './PopupBlock'

  export default {
    name: 'ItemBeer',
    components: {PopupBlock},
    props: {
      item: Object,
    },

    data: () => ({
      kek: [
        {
          "id": 1,
          "name": "Buzz",
          "tagline": "A Real Bitter Experience.",
          "first_brewed": "09/2007",
          "description": "A light, crisp and bitter IPA brewed with English and American hops. A small batch brewed only once.",
          "image_url": "https://images.punkapi.com/v2/keg.png",
          "abv": 4.5,
          "ibu": 60,
          "target_fg": 1010,
          "target_og": 1044,
          "ebc": 20,
          "srm": 10,
          "ph": 4.4,
          "attenuation_level": 75,
          "volume": {
            "value": 20,
            "unit": "litres"
          },
          "boil_volume": {
            "value": 25,
            "unit": "litres"
          },
          "method": {
            "mash_temp": [
              {
                "temp": {
                  "value": 64,
                  "unit": "celsius"
                },
                "duration": 75
              }
            ],
            "fermentation": {
              "temp": {
                "value": 19,
                "unit": "celsius"
              }
            },
            "twist": null
          },
          "ingredients": {
            "malt": [
              {
                "name": "Maris Otter Extra Pale",
                "amount": {
                  "value": 3.3,
                  "unit": "kilograms"
                }
              },
              {
                "name": "Caramalt",
                "amount": {
                  "value": 0.2,
                  "unit": "kilograms"
                }
              },
              {
                "name": "Munich",
                "amount": {
                  "value": 0.4,
                  "unit": "kilograms"
                }
              }
            ],
            "hops": [
              {
                "name": "Fuggles",
                "amount": {
                  "value": 25,
                  "unit": "grams"
                },
                "add": "start",
                "attribute": "bitter"
              },
              {
                "name": "First Gold",
                "amount": {
                  "value": 25,
                  "unit": "grams"
                },
                "add": "start",
                "attribute": "bitter"
              },
              {
                "name": "Fuggles",
                "amount": {
                  "value": 37.5,
                  "unit": "grams"
                },
                "add": "middle",
                "attribute": "flavour"
              },
              {
                "name": "First Gold",
                "amount": {
                  "value": 37.5,
                  "unit": "grams"
                },
                "add": "middle",
                "attribute": "flavour"
              },
              {
                "name": "Cascade",
                "amount": {
                  "value": 37.5,
                  "unit": "grams"
                },
                "add": "end",
                "attribute": "flavour"
              }
            ],
            "yeast": "Wyeast 1056 - American Ale™"
          },
          "food_pairing": [
            "Spicy chicken tikka masala",
            "Grilled chicken quesadilla",
            "Caramel toffee cake"
          ],
          "brewers_tips": "The earthy and floral aromas from the hops can be overpowering. Drop a little Cascade in at the end of the boil to lift the profile with a bit of citrus.",
          "contributed_by": "Sam Mason <samjbmason>"
        },
      ],
    }),

    methods: {
      decreaseStrLength(str) {
        const maxLength = 80
        if (str.length > maxLength) {
          return str = str.substr(0, maxLength) + '...'
        }
        return str
      }
    }
  }
</script>

<style>
.text {
  padding: 10px;
}
</style>
