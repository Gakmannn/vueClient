<template>
  <h1>Posts</h1>
    <div id="content">
      <template v-for="post of data" :key="post.id">
        <PostComponent :post="post" emoji="😁" :countChars="countChars"/>
      </template>
    </div>
    <div style="margin: 20px 0; text-align: center;">
      <button id="add" @click="router.push('/add_post')">'add post'</button>
    </div>

</template>

<script setup lang="ts">
import router from '@/router'
import PostComponent from '@/components/PostComponent.vue'
import { ref } from 'vue'

const addPost = ref(false)
const data = ref({} as any)

function countChars (text:string) {
  return text.length
}

async function getPosts() {
  const resp = await fetch("http://localhost:3001/posts")
  data.value = (await resp.json()).data
}
getPosts()
</script>

<style>
body {
      margin: 0 auto;
      padding: 0;
      max-width: 600px;
      background-color: antiquewhite;
    }
</style>