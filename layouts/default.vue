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
    <v-main >
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
      <v-footer
    class="footer"
    color="grey darken-4"
    padless
  >
    <v-row
      justify="center"
      no-gutters
    >
      <v-btn
        v-for="link in links"
        :key="link"
        color="white"
        text
        rounded
        class="my-2"
      >
        {{ link }}
      </v-btn>
      <v-col
        class="grey darken-4 py-4 text-center white--text"
        cols="12"
      >
        {{ new Date().getFullYear() }} — <strong>Fridgy.App</strong>
      </v-col>
    </v-row>
  </v-footer>
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
      links: [
        'Home',
        'About Us',
        'Contact Us',
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
.footer{
  position: fixed;
  bottom:0;
  width: 100%;

}
</style>
