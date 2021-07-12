<template>
  <v-app>
    <div class="overflow-hidden">
      <v-app-bar color="grey darken-4" dark>
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
        <v-toolbar-title>My Home</v-toolbar-title>

        <v-spacer></v-spacer>
        <v-btn
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          exact
          elevation="2"
          color="transparent"
        >
          <v-icon>mdi-calendar-month</v-icon>
          {{ item.title }}
        </v-btn>
        <v-spacer></v-spacer>
        <v-btn elevation="2" color="transparent">
          <v-icon>mdi-cog-outline</v-icon>
          Settings
        </v-btn>
      </v-app-bar>
    </div>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          icon: 'mdi-calendar-month',
          title: 'Calendar',
          to: '/',
        },
        {
          icon: 'mdi-cart-outline',
          title: 'Shopping List',
          to: '/shopping',
        },
        {
          icon: 'mdi-note-outline',
          title: 'Post-Notes',
          to: '/inspire',
        },
      ],
      title: 'Vuetify.js',
    }
  },
}
</script>

<style scoped>
.white {
  color: #fff;
}
</style>
