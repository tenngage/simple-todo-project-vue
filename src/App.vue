<template>
    <div>
        <div class="name">
            <h1>todo app</h1>
        </div>
        <div>
            <TaskInput @sendTask="addTask" />
            <ul>
                <li v-for="task in taskList">
                    <TaskCard @onRemove="removeTask(task.id)" @onDone="setDoneTask(task.id)" :task="task" />
                </li>
            </ul>
            
        </div>
    </div>
</template>

<script setup>
import TaskInput from './components/TaskInput.vue';
import TaskCard from './components/TaskCard.vue';
import {ref, onMounted} from 'vue';

// let taskList = ref('');

const taskList = ref([]);

onMounted(() => {
    if (!localStorage.getItem('data') || localStorage.getItem('data') == []) {
        taskList.value = [{
            id: 0,
            title: 'Create Project',
            description: 'Gather your strength',
            status: false
        }];
        return;
    }
    const data = localStorage.getItem('data');
    taskList.value = JSON.parse(data);
});

// const computedId = computed(() => taskList.value[taskList.value.length - 1].id + 1);

function addTask({title, description}) {
    taskList.value.push({
        id: taskList.value[taskList.value.length - 1].id + 1,
        title,
        description,
        status: false
    });
    const data = JSON.stringify(taskList.value);
    localStorage.setItem('data', data);
}

function setDoneTask(id) {
    taskList.value = taskList.value.map(x => {
        if (x.id === id) {
            x.status = true;
            x.description = 'Done!';
        }
        return x;
    });
    const data = JSON.stringify(taskList.value);
    localStorage.setItem('data', data);
}

function removeTask(id) {
    taskList.value = taskList.value.filter(x => x.id !== id);
    const data = JSON.stringify(taskList.value);
    localStorage.setItem('data', data);
}

</script>

<style scoped>
h1 {
    color: rgb(230, 230, 230);
    font-size: 55px;
}

.name {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 10px;
}

ul {
    list-style: none;
}
</style>

