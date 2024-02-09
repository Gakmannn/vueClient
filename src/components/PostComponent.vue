<template>
  <div class="post">
    <h2>{{post.title}} {{ emoji }}</h2>
    <p>{{post.content}}</p>
    <p>{{ countChars(post.content)}}</p>
    <div style="display: flex; justify-content: space-between;">
      <p>{{post.author.email}}, {{new Date(post.created_at).toLocaleDateString()}}</p>
      <p>{{ post.categories.map((cat: any) => '#' + cat.name.replaceAll(' ', '_')).toString() }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps(['post', 'emoji', 'countChars'])
</script>

<style scoped lang="scss">
  .post {
    border: 1px solid black;
    border-radius: 20px;
    padding: 10px;
    h2 {
      text-align: center;
    }
  }
</style>
