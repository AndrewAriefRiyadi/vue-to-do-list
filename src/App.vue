<script setup>
import { ref } from 'vue'
import modalCreate from './components/modalCreate.vue'
import itemList from './components/itemList.vue'

const isModalOpen = ref(false);
const completed = ref(false);
</script>

<template>

  <body class="bg-gray-900 font-mono py-28 lg:px-64 md:px-48">
    <div class="h-screen flex flex-col gap-4">
      <p class="text-white text-2xl text-center">To-Slay List</p>
      <!-- Buttons -->
      <div class="flex justify-around">
        <button @click="isModalOpen = true"
          class="w-fit px-3 py-1 outline-1 text-white outline-gray-700 bg-green-800 rounded-2xl hover:bg-green-700 hover:outline-gray-900 transition">Create</button>
      </div>
      <itemList :task="'Bunuh Goblin'" :completed="completed" @update:completed="completed = $event" />
    </div>
    <!-- Modal Create -->
    <modalCreate :visible="isModalOpen" @close="isModalOpen = false" />
  </body>
</template>
