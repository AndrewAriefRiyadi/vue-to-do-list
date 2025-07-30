<!-- modalCreate.vue -->
<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  visible: Boolean
})

const emit = defineEmits(['close']) // jika ingin close dari dalam modal

const text = ref('Belikan susu untuk anak! Jangan lupa Pulang!')
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
        <textarea v-model="text" class="text-white w-full px-2 py-1 bg-gray-950 rounded resize-none"
          rows="4"></textarea>
      </div>

      <div class="flex justify-end gap-2">
        <button @click="$emit('close')" class="bg-gray-600 text-white px-4 py-1 rounded hover:bg-gray-500 transition">
          Cancel
        </button>
        <button class="bg-green-800 text-white px-4 py-1 rounded hover:bg-green-700 transition">
          Summon!
        </button>
      </div>
    </div>
  </div>
</template>
