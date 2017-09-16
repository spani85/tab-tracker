<template>
  <v-layout column>
    <v-flex xs6 offset-xs3>
      <panel title="Login">
        <form>
          <v-text-field
            label="Email" 
            v-model="email"
            ></v-text-field>
          <br>
          <v-text-field            
            v-model="password"
            type="password"
            label="Password"
            ></v-text-field>
        </form>
        <br>
        <v-alert error value="true" v-if="error" v-html="error"></v-alert>
        <br>
        <v-btn class="cyan" dark @click="login">Login</v-btn>
      </panel>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async login () {
      try {
        const response = await AuthenticationService.login({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
        this.error = null
        this.email = ''
        this.password = ''
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>

<style scoped>
</style>
