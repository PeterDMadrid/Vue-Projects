<script setup>
const emit = defineEmits(['project-selected'])

const projects = [
    'To Do App',
    'Random Quote Generator',
    'Noob Calculator',
    'Project 4',
    'Project 5',
    'Project 6',
    'Project 7',
    'Project 8',
    'Project 9',
    'Project 10'
]

const selectProject = (project) => {
    emit('project-selected', project)
}
</script>

<template>
    <div class="border p-4 m-4 bg-white rounded-lg shadow-md w-full h-136 overflow-y-auto">
        <h1 class="text-xl font-bold mb-4">Project Selection</h1>
        <ul class="space-y-1">
            <li v-for="(project, index) in projects" :key="index">
                <button @click="selectProject(project)"
                    class="w-full text-left p-2 rounded hover:bg-blue-100 border border-gray-200 transition-colors cursor-pointer">{{
                        project
                    }}</button>
            </li>
        </ul>
    </div>
</template>