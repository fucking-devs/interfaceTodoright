<template>
    <div class="task-container">
 <h2>Задачи</h2>
 <form @submit.prevent="addTask">
 <input v-model="newTaskTitle" placeholder="Название задачи" required />
 <button type="submit">Добавить задачу</button>
  </form>
     <ul>
     <li v-for="task in tasks" :key="task._id">
     {{ task.title }} - {{ task.completeness ? 'Выполнено' : 'Не выполнено' }}
 <button @click="toggleCompleteness(task)">Изменить статус</button>\
 <button @click="deleteTask(task._id)">Удалить</button>
     </li>
   </ul>
    </div>
  </template>
  <script>
  import { ref } from 'vue';
  import axios from 'axios';
  export default {
    setup() {
          const tasks = ref([]);
    const newTaskTitle = ref('');
    const fetchTasks = async () => {
  const response = await axios.get('/api/tasks');
        tasks.value = response.data;};
      const addTask = async () => {
        await axios.post('/api/tasks', { title: newTaskTitle.value });
        newTaskTitle.value = '';
        fetchTasks();
      };
      const toggleCompleteness = async (task) => {
        await axios.put(`/api/tasks/${task._id}`, { completeness: !task.completeness });
        fetchTasks();
      };
      const deleteTask = async (id) => {
        await axios.delete(`/api/tasks/${id}`);
        fetchTasks();
      };
      fetchTasks();
      return { tasks, newTaskTitle, addTask, toggleCompleteness, deleteTask };
    },
  };
  </script>
  
  <style scoped>
  .task-container {
    border: 1px solid #ccc;
    padding: 20px;
    margin: 10px;
  }
  h2 {
    color: #333;
  }
  form {
    margin-bottom: 10px;
  }
  input {
    margin-right: 10px;
  }
  </style>
  