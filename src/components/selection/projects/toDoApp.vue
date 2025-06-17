<script setup>
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([])
const taskNumber = ref(1)

const addTask = () => {
    if (newTask.value.trim() !== '') {
        tasks.value.push(
            {
                id: taskNumber.value,
                text: newTask.value
            }
        )
        newTask.value = ''
        taskNumber.value++
        console.log(tasks.value)
    }
}

const removeTask = (index) => {
    tasks.value.splice(index, 1)
}

</script>

<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">To Do App</h1><br>
        <hr><br>

        <div class="pt-4 pb-4">
            <input class="border mr-2 pt-2 pb-2" type="text" v-model="newTask" @keyup.enter="addTask">
            <button class="border bg-gray-600 text-green-500 p-2 cursor-pointer" @click="addTask">Add</button>
        </div>

        <p class="text-blue-600 mt-2">List of Tasks:</p>
        <ul>
            <li v-for="(task, index) in tasks" :key="index" class="flex justify-between">
                <p>{{ task.id }}. {{ task.text }}</p>
                <button class="bg-gray-600 border mb-2 pr-2 pl-2 text-red-500 cursor-pointer"
                    @click="removeTask(index)">Del</button>
            </li>
        </ul>
    </div>
</template>