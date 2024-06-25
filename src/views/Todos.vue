<template>
    <div class="container">
      <h1 class="title">Daftar Kegiatan</h1>
      <div class="input-container">
        <input v-model="input_content" @keyup.enter="addTodo" placeholder="Nama Kegiatan" class="input" />
        <button @click="addTodo" class="add-button">Tambahkan Kegiatan</button>
      </div>
      <ul class="activities-list">
        <li v-for="(todo, index) in filteredTodos" :key="index" class="activity-item">
          <span v-if="todo.done" class="check-icon">✅</span>
          <span :class="{ completed: todo.done }" class="activity-content">{{ todo.content }}</span>
          <div class="buttons">
            <button @click="todo.done = !todo.done" class="action-button">
              {{ todo.done ? 'Uncheck' : 'Checklist' }}
            </button>
            <button @click="removeTodo(todo)" class="action-button">Hapus</button>
          </div>
        </li>
      </ul>
      <button @click="filterCompleted = !filterCompleted" class="filter-button">
        {{ filterCompleted ? 'Tampilkan Semua Kegiatan' : 'Tampilkan Kegiatan Yang Belum Selesai' }}
      </button>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  
  const input_content = ref('')
  const filterCompleted = ref(false)
  const todos = ref([])
  
  const todos_asc = computed(() => todos.value.sort((a, b) => b.createdAt - a.createdAt))
  const filteredTodos = computed(() => filterCompleted.value ? todos_asc.value.filter(todo => !todo.done) : todos_asc.value)
  
  const addTodo = () => {
    if (input_content.value.trim() === '') return
    todos.value.push({ content: input_content.value, done: false, createdAt: new Date().getTime() })
    input_content.value = ''
  }
  
  const removeTodo = todo => {
    const index = todos.value.findIndex(t => t === todo)
    if (index !== -1) todos.value.splice(index, 1)
  }
  </script>
  
  <style scoped>
  .container {
    max-width: 800px;
    margin: 0 auto;
    margin-top: 50px;
    padding: 20px;
    background: #fdf3e7;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    font-family: 'Arial', sans-serif;
  }
  
  .title {
    font-size: 24px;
    color: #6b4f4f;
    margin-bottom: 20px;
    text-align: center;
  }
  
  .input-container {
    display: flex;
    margin-bottom: 20px;
  }
  
  .input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-right: 10px;
    background-color: #fff;
  }
  
  .add-button {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    background-color: #d9a065;
    color: white;
    cursor: pointer;
  }
  
  .activities-list {
    list-style: none;
    padding: 0;
  }
  
  .activity-item {
    display: flex;
    align-items: center;
    padding: 15px;
    border-bottom: 1px solid #eee;
  }
  
  .check-icon {
    margin-right: 10px;
  }
  
  .activity-content {
    flex: 1;
    font-size: 16px;
    color: #6b4f4f;
  }
  
  .activity-content.completed {
    text-decoration: line-through;
    color: #999;
  }
  
  .buttons {
    display: flex;
    gap: 10px;
  }
  
  .action-button {
    padding: 5px 10px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    background-color: #a07658;
    color: white;
  }
  
  .filter-button {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    background-color: #d9a065;
    color: white;
    cursor: pointer;
    margin-top: 20px;
  }
  </style>
  