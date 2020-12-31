<template>
  <div>
    <form @submit.prevent="login">
      <label for="email">Email:</label>
      <input
        type="email"
        v-model="email"
        name="email"
        value
      >

      <label for="password">Password:</label>
      <input
        type="password"
        v-model="password"
        name="password"
        value
      >

      <button
        type="submit"
        name="button"
      >Login</button>

      <p>{{error}}</p>

      <router-link to="/register">
        Don't have an account? Register.
      </router-link>
    </form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        error: null,
        email: '',
        password: ''
      };
    },
    methods: {
      login() {
        this.$store
          .dispatch( 'login', { email: this.email, password: this.password } )
          .then( () => {
            this.$router.push( { name: 'dashboard' } );
          } )
          .catch(
            ( {
              response: {
                data: { error }
              }
            } ) => {
              console.log( error );
              this.error = error;
            }
          );
      }
    }
  };
</script>

<style>
</style>
