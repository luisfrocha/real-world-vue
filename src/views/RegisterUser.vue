<template>
  <div>
    <form @submit.prevent="register">
      <label for="name">Name:</label>
      <input
        type="text"
        v-model="name"
        name="name"
        value
      >

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
      >Register</button>

      <ul>
        <li
          v-for="(error,index) in errors"
          :key="index"
        >{{error}}</li>
      </ul>
      <router-link to="/login">
        Already have an account? Login.
      </router-link>
    </form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        name: '',
        email: '',
        password: '',
        errors: null
      };
    },
    methods: {
      register() {
        this.$store
          .dispatch( 'register', {
            name: this.name,
            email: this.email,
            password: this.password
          } )
          .then( () => {
            this.$router.push( { name: 'dashboard' } );
          } )
          .catch(
            ( {
              response: {
                data: { errors }
              }
            } ) => {
              console.log( errors );
              this.errors = errors;
            }
          );
      }
    }
  };
</script>

<style>
</style>
