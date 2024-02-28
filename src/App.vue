<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
if (location.pathname != '/login'){
  if (!localStorage.id || localStorage.id == 'undefined' || !localStorage.uuid || localStorage.uuid == 'undefined') {
    location.replace('/login')
  } else {
    // console.log('check')
    checkUser()
  }

  // теперь ошибок нет

  async function checkUser() {
    const resp = await fetch("http://localhost:3001/check_user", {
      method: "post",
      headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        id: +localStorage.id,
        uuid: localStorage.uuid
      })
    })
    const data = await resp.json()
    // console.log(data.data)
    if (!data.data) {
      localStorage.removeItem('id')
      localStorage.removeItem('uuid')
      location.replace('/login')
    }
  }
}
</script>

<template>
  <RouterView />
</template>

<style scoped></style>
