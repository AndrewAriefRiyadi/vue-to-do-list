<!-- modalCreate.vue -->
<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  visible: Boolean
});

const emit = defineEmits(['close','submitted']); // jika ingin close dari dalam modal

const title = ref('Belikan susu untuk anak! Jangan lupa Pulang!');

const loading = ref(false)
const error = ref(null)


const submit = async () => {

  try {
    const response = await fetch('http://localhost:8000/lists', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        title: title.value,
        completed: false
      })
    })
    if (!response.ok) throw new Error('Gagal mengirim data')

    const result = await response.json()
    console.log('Success:', result)
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
    emit('submitted');
    emit('close');
  }
};

</script>

<template>
  <div v-if="visible" class="fixed inset-0 z-50 flex items-center justify-center">
    <!-- Background hitam transparan -->
    <div class="absolute inset-0 bg-black opacity-50"></div>
    <!-- Konten modal -->
    <div
      class="relative bg-gray-900 outline-white outline-1 p-4 w-full max-w-3xl flex flex-col justify-center gap-2 rounded-md shadow-lg">
      <p class="text-white text-lg font-semibold">Create Monster!?</p>
      <div>
        <textarea v-model="title" class="text-white w-full px-2 py-1 bg-gray-950 rounded resize-none"
          rows="4"></textarea>
      </div>
      <div class="flex justify-end gap-2">
        <button @click="$emit('close')" class="bg-gray-600 text-white px-4 py-1 rounded hover:bg-gray-500 transition">
          Cancel
        </button>
        <button @click="submit()" class="bg-green-800 text-white px-4 py-1 rounded hover:bg-green-700 transition">
          Summon!
        </button>
      </div>
    </div>
  </div>
</template>
