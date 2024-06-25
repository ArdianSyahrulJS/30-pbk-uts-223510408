<template>
    <div class="container">
      <h1 class="title">Daftar Posts</h1>
      <label for="user-select" class="label">Filter by User:</label>
      <select id="user-select" v-model="selectedUser" class="select">
        <option value="">All Users</option>
        <option v-for="user in users" :key="user.id" :value="user.id">
          {{ user.name }}
        </option>
      </select>
      <ul class="posts-list">
        <li v-for="post in filteredPosts" :key="post.id" class="post-item">
          <h2 class="post-title">{{ post.title }}</h2>
          <p class="post-body">{{ post.body }}</p>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref, computed, onMounted } from 'vue'
  
  const selectedUser = ref(null)
  const users = ref([])
  const posts = ref([])
  const loading = ref(true)
  
  const filteredPosts = computed(() => {
    if (!selectedUser.value) return posts.value
    return posts.value.filter(post => post.userId === selectedUser.value)
  })
  
  onMounted(async () => {
    const usersResponse = await fetch('https://jsonplaceholder.typicode.com/users')
    const postsResponse = await fetch('https://jsonplaceholder.typicode.com/posts')
    users.value = await usersResponse.json()
    posts.value = await postsResponse.json()
    loading.value = false
  })
  </script>
  
  <style scoped>
  .container {
    max-width: 1000px;
    margin: 0 auto;
    margin-top: 50px;
    margin-bottom: 50px;
    padding: 20px;
    background: #fdf3e7;
    box-shadow: 5px 5px 8px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    font-family: 'Arial', sans-serif;
  }
  
  .title {
    font-size: 24px;
    color: #6b4f4f;
    margin-bottom: 20px;
    text-align: center;
  }
  
  .label {
    display: block;
    margin-bottom: 10px;
    font-size: 16px;
    color: #6b4f4f;
  }
  
  .select {
    width: 100%;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-bottom: 20px;
    background-color: #fff;
  }
  
  .posts-list {
    list-style: none;
    padding: 0;
  }
  
  .post-item {
    padding: 15px;
    border-bottom: 1px solid #eee;
  }
  
  .post-title {
    font-size: 20px;
    color: #6b4f4f;
    margin-bottom: 10px;
  }
  
  .post-body {
    font-size: 16px;
    color: #6b4f4f;
  }
  </style>
  