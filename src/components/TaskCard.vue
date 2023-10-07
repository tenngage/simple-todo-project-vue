<template>
    <div class="container">
        <div>
            <h4>{{ task.title }}</h4>
            <p :class="{ done: task.status }">{{ task.description }}</p>
        </div>
        <div>
            <button @click="onDone" v-if="!task.status" class="check-mark">&#10003;</button>
            <button @click="onRemove" v-else class="x-mark">&#10060;</button>
        </div>
    </div>
</template>

<script setup>
// import {ref} from 'vue';

const emit = defineEmits(['onDone', 'onRemove']);

defineProps({
    task: {
        required: true,
        default: {
            id: 0,
            title: 'Create Project',
            description: 'Gather your strength',
            status: false
        }
    }
});

function onDone() {
    emit('onDone');
};

function onRemove() {
    emit('onRemove');
};

</script>

<style scoped>
.x-mark, .check-mark {
    background-color: black;
    width: 25px;
    height: 25px;
    cursor: pointer;
}

.check-mark {
    color: rgb(0, 255, 0);
}

.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 5px;
    border: 1px rgb(77, 77, 77) solid;
    background-color: rgb(199, 199, 199);
    padding: 10px 20px;
    margin-bottom: 2px;
}

.done {
    color: rgb(0, 160, 0);
    font-weight: 700;
}
</style>