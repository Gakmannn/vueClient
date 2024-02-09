<script setup lang="ts">
import axios from 'axios'
import { ref } from 'vue'
const title = ref('')
const content = ref('')

const addPostClick = async () => {
  await axios.post('http://localhost:3001/posts', {
    title: title.value,
    content: content.value,
    author_id: +localStorage.id
  })
  location.assign('/')
}

</script>

<template>
  <div id="addPost" style="text-align: center;">
    <div style="display: flex; flex-direction: column; gap:10px; margin-bottom: 10px;">
      <input id="newTitle" v-model="title" type="text" placeholder="title">
      <textarea id="newContent" v-model="content" cols="30" rows="10" placeholder="content"></textarea>
    </div>
    <button id="addPostButton" @click="addPostClick">Save</button>
  </div>
</template>

<style></style>
