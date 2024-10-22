<template>
  <v-card flat elevation="0" width="400" color="#E5D9F2">
    <v-card-title>
      <p class="text-center" color="#A594F9" style="width: 100% !important;">
        Bienvenido a mi empresa.
      </p>
    </v-card-title>
    <v-card-text>
      <v-row style="width: 100% !important;">
        <v-col cols="4">
          <v-img :src="require('@/assets/images/mj.jpg')" />
        </v-col>
        <v-col>
          <form>
            <v-row>
              <v-text-field
                v-model="form.usuario"
                outlined
                dense
              />
            </v-row>
            <v-row>
              <v-text-field
                v-model="form.password"
                type="password"
                outlined
                dense
              />
            </v-row>
            <v-row v-if="errorMessage" class="error">
              {{ errorMessage }}
            </v-row>
          </form>
        </v-col>
      </v-row>
    </v-card-text>
    <v-card-actions>
      <v-row align="center" justify="center" class="ma-3">
        <v-btn color="#F5eFFF" @click="gotoSignUp">
          <span style="text-transform: none; color: #6C48C5;">
            Registrarse
          </span>
        </v-btn>
        <v-btn color="#CDC1FF" class="ml-4" @click="login">
          <span style="text-transform: none; color: #6C48C5;">
            Iniciar Sesion
          </span>
        </v-btn>
      </v-row>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data () {
    return {
      form: {
        usuario: '',
        password: ''
      },
      errorMessage: ''
    }
  },
  methods: {
    async login () {
      try {
        const res = await this.$auth.loginWith('local', {
          data: this.form
        })
        console.log('@@ res => ', res)
      } catch (error) {
        this.errorMessage = error
      }
    },
    gotoSignUp () {
      this.$router.push('/signup')
    }
  }
}
</script>

<style scoped>
.error {
  color: red;
}
</style>
