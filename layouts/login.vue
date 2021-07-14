<template>
  <v-app class="fond">
    <v-main >
      <v-container class="hola">
        <Nuxt />
      </v-container>
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
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      links: [
        'Home',
        'About Us',
        'Contact Us',
      ]
    }
  }
}
</script>

<style scoped>

.fond{
  background-image: url('@/static/FridgeWallpaper.jpg');
  background-repeat: no-repeat;
  background-size:cover;
}
.hola{
  display: flex;
  justify-content: center;  
}
.footer{
  position: fixed;
  bottom:0;
  width: 100%;

  
}

</style>