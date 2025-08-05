<script setup>
import { onMounted, ref } from 'vue'
import modalCreate from './components/modalCreate.vue'
import itemList from './components/itemList.vue'
import axios from 'axios';

const isModalOpen = ref(false);
const completed = ref(false);

const todos = ref([]);

const fetchTodos = async () => {
  try {
    const res = await axios.get('http://localhost:8000/lists')
    todos.value = res.data
  } catch (error) {
    todos.value = []
    console.error('Gagal mengambil data:', error)
  }
};

onMounted(()=> {
  fetchTodos()
});

</script>
<template>
  <body class="bg-gray-900 font-mono py-28 lg:px-64 md:px-48">
    <div class="h-screen flex flex-col gap-4">
      <p class="text-white text-2xl text-center">To-Slay List</p>
      <!-- Buttons -->
      <div class="flex justify-around">
        <button @click="isModalOpen = true" @submitted="fetchTodos()"
          class="w-fit px-3 py-1 outline-1 text-white outline-gray-700 bg-green-800 rounded-2xl hover:bg-green-700 hover:outline-gray-900 transition">Create</button>
      </div>
      <div  v-for="todo in todos" :key="todo.id">
        <itemList :id="todo.ID" :task="todo.title" :completed="todo.completed"  @updated="fetchTodos()"/>
      </div>
    </div>
    <!-- Modal Create -->
    <modalCreate :visible="isModalOpen" @close="isModalOpen = false" @submitted="fetchTodos()" />
  </body>
</template>
