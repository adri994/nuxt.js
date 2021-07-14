<template>
  <v-container fluid >
    <v-row no-gutters>
      <v-col cols="5" offset="-3" class="mt=3">
        <ProductsList
          @moveShopping="addList"
          v-if="product.length > 0"
          :products="product"
        />
        <v-container>
          <v-card class="d-flex flex-column justify-center">
            <v-text-field
              v-model="nameProduct"
              label="Products"
              outlined
              clearable
            ></v-text-field>
            <v-btn x-large color="#1E88FF" dark depressed>
              Add New Product
            </v-btn>
          </v-card>
        </v-container>
        <v-spacer></v-spacer>
      </v-col>
      <v-col
        v-if="list.length > 0"
        offset="2"
        class="d-flex flex-column justify-center"
        cols="4"
      >
        <ShoppingList @isbuy="changeList" :list="list" />
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  async asyncData({ $axios }) {
    const [listProduct, shoppingList] = await Promise.all([
      $axios.$get('/api/products'),
      $axios.$get('/api/shoppingList'),
    ])
    return { apiProduct: listProduct, apiShopping: shoppingList }
  },
  data() {
    return {
      list: [],
      product: [],
      nameProduct: '',
    }
  },
  mounted() {
    this.product = this.apiProduct
    this.list = this.apiShopping
  },
  methods: {
    async addList(product) {
      this.list = await this.$axios.$post('/api/shoppingList/addProduct', {
        productId: product._id,
      })
    },
    changeList(items) {
      this.list = [items]
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