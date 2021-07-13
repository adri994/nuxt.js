<template>
  <v-container fluid>
    <v-row no-gutters>
      <v-card
        class="mx-auto scroll"
        max-width="500"
        max-height="600"
        overflow-visible
      >
        <v-app-bar color="#1E88FF" dark class="app_bar">
          <v-spacer></v-spacer>
          <v-toolbar-title><b>PRODUCTS</b></v-toolbar-title>
          <v-spacer></v-spacer>
        </v-app-bar>

        <v-list>
          <v-list-group
            v-for="item in listProduct"
            :key="item.title"
            v-model="item.active"
            :prepend-icon="item.action"
            no-action
          >
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title
                  v-text="item.title"
                  class="title"
                ></v-list-item-title>
              </v-list-item-content>
            </template>

            <v-list-item
              v-for="child in item.items"
              @click="addProduct(child)"
              :key="child.name"
            >
              <v-list-item-content>
                <v-list-item-title v-text="child.name"></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-group>
        </v-list>
      </v-card>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: {
    products: Array,
  },
  data: () => ({
    items: [
      {
        action: 'mdi-fruit-pineapple',
        items: [],
        title: 'Fruits & Vegetables',
        uid: '60e5853e7435c4c3713e1471',
      },
      {
        action: 'mdi-baguette',
        active: true,
        items: [],
        title: 'Bread & Cakes',
        uid: '60e585bb7435c4c3713e1475',
      },
      {
        action: 'mdi-cheese',
        active: true,
        items: [],
        title: 'Milk & Cheese',
        uid: '60e585d67435c4c3713e1476',
      },
      {
        action: 'mdi-fish',
        active: true,
        items: [],
        title: 'Fish',
        uid: '60e585f47435c4c3713e1477',
      },
      {
        action: 'mdi-food-steak',
        active: true,
        items: [],
        title: 'Meat',
        uid: '60e5860b7435c4c3713e1478',
      },
      {
        action: 'mdi-shaker-outline',
        active: true,
        items: [],
        title: 'Ingredients & Spices',
        uid: '60e586277435c4c3713e1479',
      },
      {
        action: 'mdi-ice-cream',
        active: true,
        items: [],
        title: 'Frozen & Pre-Cooked Food',
        uid: '60e5863e7435c4c3713e147a',
      },
      {
        action: 'mdi-pasta',
        active: true,
        items: [],
        title: 'Cereals & Pasta',
        uid: '60e586567435c4c3713e147b',
      },
      {
        action: 'mdi-cookie',
        active: true,
        items: [],
        title: 'Snacks & Sweets',
        uid: '60e586b87435c4c3713e147c',
      },
      {
        action: 'mdi-beer',
        active: true,
        items: [],
        title: 'Drinks',
        uid: '60e586d87435c4c3713e147e',
      },
      {
        action: 'mdi-spray-bottle',
        active: true,
        items: [],
        title: 'Home',
        uid: '60e586eb7435c4c3713e147f',
      },
      {
        action: 'mdi-bottle-tonic-plus',
        active: true,
        items: [],
        title: 'Cleanliness & Health',
        uid: '60e586fa7435c4c3713e1480',
      },
      {
        action: 'mdi-paw',
        active: true,
        items: [],
        title: 'Pet Products',
        uid: '60e587167435c4c3713e1481',
      },
      {
        action: 'mdi-shovel',
        active: true,
        items: [],
        title: 'Garden & Home',
        uid: '60e5872d7435c4c3713e1482',
      },
      {
        action: 'mdi-account',
        active: true,
        items: [],
        title: 'Own Products',
        uid: '60e587407435c4c3713e1483',
      },
    ],
  }),
  computed: {
    listProduct() {
      this.addProducts()
      return this.items
    },
  },
  methods: {
    addProducts() {
      this.products.forEach((product) => {
        this.items.forEach((categ) => {
          if (categ.uid === product.category)
            categ.items = [...categ.items, product]
        })
      })
    },
    addProduct(product) {
      this.$emit('moveShopping', product)
    },
  },
}
</script>

<style scoped>
.scroll {
  overflow: scroll;
}
.title {
  font-family: 'Raleway', sans-serif !important;
  color: #0066da;
}
::-webkit-scrollbar {
  display: none;
}
.app_bar {
  max-height: calc(100vh - 64px);
  height: auto;
  overflow-y: auto;
  overflow-x: hidden;
}
</style>