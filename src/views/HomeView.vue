<template>
  <h1>Posts</h1>
    <div id="content" v-html="Content">
      
    </div>
    <div style="margin: 20px 0; text-align: center;">
      <button id="add" @click="addPost=!addPost">{{ addPost?'hide':'add post'}}</button>
    </div>

    <div v-if="addPost" id="addPost" style="text-align: center;">
      <div style="display: flex; flex-direction: column; gap:10px; margin-bottom: 10px;">
        <input id="newTitle" v-model="title" type="text" placeholder="title">
        <textarea id="newContent" v-model="content" cols="30" rows="10" placeholder="content"></textarea>
      </div>
      <button id="addPostButton" @click="addPostClick">Save</button>
    </div>
</template>

<script setup lang="ts">
// import router from '@/router'
import axios from 'axios'
import { ref } from 'vue'

const addPost = ref(false)
const title = ref('')
const content = ref('')
const Content = ref('')

const addPostClick = async () => {
  await axios.post('http://localhost:3001/posts', {
    title: title.value,
    content: content.value,
    author_id: +localStorage.id
  })
  location.reload()
}

async function getPosts() {
  const resp = await fetch("http://localhost:3001/posts")
  const data = await resp.json()
  let textContent = ''
  console.log(data.data)
  for (let el of data.data) {
    textContent += `
          <div>
            <h2>${el.title}</h2>
            <p>${el.content}</p>
            <div style="display: flex; justify-content: space-between;">
              <p>${el.author.email}, ${new Date(el.created_at).toLocaleDateString()}</p>
              <p>${el.categories.map((cat:any) => '#' + cat.name.replaceAll(' ', '_'))}</p>
            </div>
          </div>
        `
  }
  Content.value = textContent
}
getPosts()
</script>

<style scoped>
body {
      margin: 0 auto;
      padding: 0;
      max-width: 600px;
      background-color: antiquewhite;
    }
</style>