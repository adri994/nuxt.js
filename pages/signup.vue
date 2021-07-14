<template>
<v-container>
  <v-form  class="post-it" ref="form" v-model="valid" lazy-validation>
    <v-text-field
      v-model="username"
      label="Username"
      required
    ></v-text-field>
    <v-menu
        ref="menu"
        v-model="menu"
        :close-on-content-click="false"
        :return-value.sync="date"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="date"
            label="BirthDay"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="date"
          no-title
          scrollable
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="menu = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.menu.save(date)"
          >
            OK
          </v-btn>
        </v-date-picker>
      </v-menu>

    <v-text-field
      v-model="email"
      :rules="emailRules"
      label="E-mail"
      required
    ></v-text-field>
    <v-text-field
      v-model="email"
      :rules="emailRules"
      label="Confirm E-mail"
      required
    ></v-text-field>
    <v-text-field
      v-model="password"
      :rules="passwordRules"
      label="Password"
      required
    ></v-text-field>
    <v-text-field
      v-model="password"
      :rules="passwordRules"
      label="Confirm Password"
      required
    ></v-text-field>

    


    <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
      Sign Up
    </v-btn>
  </v-form>
</v-container>

</template>
<script>
export default {
  layout: 'login',
  data: () => ({
    date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
      menu: false,
      modal: false,
      menu2: false,
    valid: true,
    password: '',
    passwordRules: [
      (v) => !!v || 'Password is required',
      (v) => (v && v.length >= 6) || 'Name must be less than 6 characters',
    ],
    email: '',
    emailRules: [
      (v) => !!v || 'E-mail is required',
      (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
  }),

  methods: {
    async validate() {
      this.$refs.form.validate()
      if (this.password !== '' && this.email !== '') {
        const hola = await this.$axios.$post('/api/auth/login', {
          email: this.email,
          password: this.password,
        })
        console.log(hola)
      }
    },
  },
}
</script>

<style scoped>

@import url(https://fonts.googleapis.com/css?family=Permanent+Marker);
.post-it {
 	width:400px;
  height:600px;
  position:relative;
  background:#ffa;
  overflow:hidden;
  margin:150px auto;
  padding:20px;
  border-radius:0 0 0 30px/45px;
  box-shadow:
    inset 0 -40px 40px rgba(0,0,0,0.2),
    inset 0 25px 10px rgba(0,0,0,0.2),
    0 5px 6px 5px rgba(0,0,0,0.2);
  font-family: 'Permanent Marker', cursive;
  line-height:1.7em;
  font-size:19px;
  -webkit-mask-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAIAAACQd1PeAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAA5JREFUeNpiYGBgAAgwAAAEAAGbA+oJAAAAAElFTkSuQmCC);
}


</style>