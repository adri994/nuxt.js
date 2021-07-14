<template>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-text-field
        v-model="email"
        :rules="emailRules"
        label="E-mail"
        required
      ></v-text-field>
      <v-text-field
        v-model="password"
        :rules="passwordRules"
        label="Password"
        required
      ></v-text-field>
      <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
        Validate
      </v-btn>
    </v-form>
  <!-- <v-form ref="form" v-model="valid" lazy-validation>
    <v-text-field
      v-model="email"
      :rules="emailRules"
      label="E-mail"
      required
    ></v-text-field>
    <v-text-field
      v-model="password"
      :rules="passwordRules"
      label="Password"
      required
    ></v-text-field>
    <v-text-field v-model="name" label="name" required></v-text-field>
    <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
      Validate
    </v-btn>
  </v-form> -->
</template>
<script>
export default {
  layout: 'login',
  data: () => ({
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
    name: '',
  }),

  methods: {
    async validate() {
      this.$refs.form.validate()
      if (this.password !== '' && this.email !== '') {
        try {
          // const hola = await this.$axios.$post('/api/auth/login', {
          //   email: this.email,
          //   password: this.password,
          // })

          const res = await this.$auth.loginWith('local',{
            data:{
              email: this.email,
              password: this.password
            }
          })
          this.$auth.$storage.setUniversal('userId', res.data.uid)

        } catch (error) {
          console.log(error)
        }
      }
    },
  },
}
</script>



