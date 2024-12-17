<template>
 <div class="queue-container">
 <h2>Очереди</h2>
 <form @submit.prevent="addQueue">
 <input v-model="newQueueTitle" placeholder="Название очереди" required />
  <button type="submit">Добавить очередь</button>
 </form>
 <ul>
 <li v-for="queue in queues" :key="queue._id">
    {{ queue.title }}
 <button @click="deleteQueue(queue._id)">Удалить</button>
 </li>
</ul>
</div>
</template>

  <script>
  import { ref } from 'vue';
  import axios from 'axios';
  
  export default {
 setup() {
     const queues = ref([]);
  const newQueueTitle = ref('');
    const fetchQueues = async () => {
  const response = await axios.get('/api/queue');
 queues.value = response.data;
      };
      const addQueue = async () => {
        await axios.post('/api/queue', { title: newQueueTitle.value });
        newQueueTitle.value = '';
        fetchQueues(); };
      const deleteQueue = async (id) => {
        await axios.delete(`/api/queue/${id}`);
        fetchQueues(); };
      fetchQueues();
      return { queues, newQueueTitle, addQueue, deleteQueue };
    },
  };
  </script>
  <style scoped>
  .queue-container {
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
  