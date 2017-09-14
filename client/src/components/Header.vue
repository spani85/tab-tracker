<template>
  <v-toolbar fixed class="cyan" dark>
    <v-toolbar-title class="mr-4" to="/">
      TabTracker
    </v-toolbar-title>

    <!-- TODO: implement me -->
    <v-toolbar-items>
      <v-btn 
        flat dark to="/">
        Home
      </v-btn>
      <v-btn flat dark>
        Browse
      </v-btn>
    </v-toolbar-items>

    <v-spacer></v-spacer>

    <v-toolbar-items>
      <v-btn v-if="!$store.state.isUserLoggedIn" flat dark to="login">
        Login
      </v-btn>
      <v-btn flat dark to="register">
        Sign Up
      </v-btn>
    </v-toolbar-items>

  </v-toolbar>
</template>

<script>
export default {

}
</script>

<style scoped>
</style>
