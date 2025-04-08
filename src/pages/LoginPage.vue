<script lang="ts">
import { ref, reactive } from 'vue'

export default {
  setup() {
    const { loggedIn, user, fetch: refreshSession } = useUserSession() // Inside the setup function now
    const credentials = reactive({
      email: '',
      password: '',
    })

    async function login() {
      try {
        await $fetch('/api/login', {
          method: 'POST',
          body: credentials
        })
        await refreshSession()
        await navigateTo('/')
      } catch {
        alert('Bad credentials')
      }
    }

    return {
      credentials,
      login,
    }
  }
}
</script>

<template>
   <form @submit.prevent="login">
    <input v-model="credentials.email" type="email" placeholder="Email">
    <input v-model="credentials.password" type="password" placeholder="Password">
    <button type="submit">Login</button>
   </form>
</template>
