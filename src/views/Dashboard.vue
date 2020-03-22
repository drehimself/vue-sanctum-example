<template>
  <div class="dashboard">
    <h1>Dashboard view</h1>
    <div>Email: {{ email }}</div>
    <button @click="logout">Logout</button>
  </div>
</template>

<script>
import axios from 'axios'

axios.defaults.withCredentials = true
axios.defaults.baseURL = 'http://localhost:8000'

export default {
  data() {
    return {
      email: '',
    }
  },
  mounted() {
    axios.get('/api/user').then(response => {
      this.email = response.data.email
    })
  },
  methods: {
    logout() {
      axios.post('/logout').then(response => {
        this.$router.push({ name: 'Home' })
      })
    }
  }
}
</script>
