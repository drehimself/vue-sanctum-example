<template>
  <div class="home">
    <form action="#" method="POST" @submit.prevent="login">
      <div>
        <input type="email" name="email" v-model="email" placeholder="email">
      </div>
      <div>
        <input type="password" name="password" v-model="password" placeholder="password">
      </div>
      <div>
        <button type="submit">Login</button>
      </div>
    </form>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'

axios.defaults.withCredentials = true
axios.defaults.baseURL = 'http://localhost:8000'

export default {
  name: 'Home',
  data() {
    return {
      email: '',
      password: '',
    }
  },
  methods: {
    login() {
      axios.get('/sanctum/csrf-cookie').then(response => {
        axios.post('/login', {
          email: this.email,
          password: this.password,
        })
        .then(response => {
          this.$router.push({ name: 'Dashboard' })
        })
      })
    }
  }
}
</script>
