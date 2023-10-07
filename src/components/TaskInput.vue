<template>
    <form>
        <input v-model="title" placeholder="Title" type="text">
        <input v-model="description" placeholder="Description" type="text">
        <button @click.prevent="sendTask">Add Task</button>
    </form>
</template>

<script setup>
import {ref} from 'vue';

const emit = defineEmits(['sendTask']);

const title = ref('');
const description = ref('');

function sendTask() {
    if (!title.value || !description.value) {
        alert('Make sure you filled out the Title and Description!');
        return
    }
    emit('sendTask', { title: title.value, description: description.value });
    title.value = '';
    description.value = '';
}

</script>

<style scoped>
input, button {
    width: 400px;
    border-radius: 5px;
    border: 1px rgb(77, 77, 77) solid;
    background-color: rgb(199, 199, 199);
    padding: 10px 20px;
    margin-bottom: 5px;
}

button {
    cursor: pointer;
    background-color: darkgray;
}

form {
    margin-bottom: 5px;
}
</style>