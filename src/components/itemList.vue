<script setup>
import axios from 'axios';
import { ref } from 'vue';

const props = defineProps({
    id: Number,
    task: String,
    completed: Boolean,
})

const health = ref(1) // ✅ health lokal
const emit = defineEmits(['updated'])

function swordClick() {
    if (props.completed) return;

    health.value--;
    if (health.value <= 0) {
        updateList()
    }
}

const updateList = async () => {
    try {
        const res = await axios.put('http://localhost:8000/lists/'+props.id,{
            title: props.task,
            completed : true
        });
        emit('updated')
    } catch (error) {
        console.error('Gagal meng-update data:', error)
    }
};

const deleteList = async () => {
    try {
        const res = await axios.delete('http://localhost:8000/lists/'+ props.id)
        emit('updated')
    } catch (error) {
        console.error('Gagal menghapus data:', error)
    }
};

</script>
<template>
    <div class=" flex">
        <div
            class=" w-full outline-1 outline-gray-700 bg-gray-800 text-white py-2 px-4 rounded-l hover:bg-gray-900 hover:outline-gray-500 transition">
            <div class=" flex justify-between">
                <p>{{ task }}</p>
                <div>
                    <span v-if="completed" class="text-green-500">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 inline" viewBox="0 0 20 20"
                            fill="currentColor">
                            <path fill-rule="evenodd"
                                d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.707a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414L9 13.414l4.707-4.707z"
                                clip-rule="evenodd" />
                        </svg>
                    </span>
                    <span v-else class="text-gray-400">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 inline" viewBox="0 0 20 20"
                            fill="currentColor">
                            <path fill-rule="evenodd"
                                d="M10 18a8 8 0 100-16 8 8 0 000 16zM10 16a6 6 0 110-12 6 6 0 010 12z"
                                clip-rule="evenodd" />
                        </svg>
                    </span>
                </div>
            </div>
        </div>
        <div
            class=" p-2 outline-1 outline-gray-700 bg-gray-800 text-white py-2 px-4 rounded-r hover:bg-gray-900 hover:outline-gray-500 transition" @click="swordClick()">
            <span class="select-none pointer-events-none">
                🗡️
            </span>
        </div>
        <div
            class=" p-2 outline-1 outline-gray-700 bg-gray-800 text-white py-2 px-4 rounded-r hover:bg-gray-900 hover:outline-gray-500 transition" @click="deleteList()">
            <span class="select-none pointer-events-none">
                ❌
            </span>
        </div>
    </div>
</template>