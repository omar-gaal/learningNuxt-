<script lang="ts" setup>

definePageMeta({
  middleware: ['authenticated'],
})

const { user, clear: clearSession } = useUserSession()

async function logout() {
  await clearSession()
  await navigateTo('/login')
}

</script>

<template>
 

 <viewFrontPage/>
 
 <h1>Welcome {{ user.name }}</h1>
 <button @click="logout">Logout</button>


  </template>