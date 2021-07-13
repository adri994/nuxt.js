<template>
  <v-card width="500" class="mx-auto" max-width="500" max-height="600">
    <v-toolbar color="#1E88FF" dark>
      <v-spacer></v-spacer>
      <v-toolbar-title><b>SHOPPING LIST</b></v-toolbar-title>

      <v-spacer></v-spacer>
    </v-toolbar>
    <v-list>
      <v-list-item v-for="(item, i) in shoppingList" :key="i">
        <v-list-item-content>
          <v-list-item-title v-text="item.product.name"></v-list-item-title>
          <v-form>
            <v-text-field v-model="ownProduct" label="Solo" solo></v-text-field>
            <v-btn
              @click="updateList(item)"
              class="mx-2"
              fab
              dark
              small
              color="primary"
            >
              <v-icon dark> mdi-minus </v-icon>
            </v-btn>
          </v-form>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      ownProduct: '',
    }
  },
  props: {
    list: [],
  },
  computed: {
    shoppingList() {
      return this.list[0].products.filter((buy) => !buy.bought)
    },
  },
  methods: {
    async updateList(item) {
      const listUpdate = await this.$axios.$put('/api/shoppingList/changeStatus', { id: item._id })
      this.$emit('isbuy',listUpdate)
    },
  },
}
</script>