<script setup>
import { ref } from 'vue';

const props = defineProps({
    task: String,
    completed: Boolean
})




</script>

<template>
    <div class=" w-full outline-1 outline-white text-white py-2 px-4">
        {{ task }}
    </div>

</template>