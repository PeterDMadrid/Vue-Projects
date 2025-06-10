<script setup>
import { ref } from 'vue'
import projectSelection from './selection/projectSelection.vue';
import displaySelected from './render/displaySelected.vue';

const selectedProject = ref('')

const handleProjectSelect = (project) => {
    selectedProject.value = project
}

</script>

<template>
    <div class="flex justify-center items-center min-h-screen min-h-screen p-8 gap-4">
        <projectSelection @project-selected="handleProjectSelect" />
        <displaySelected :selected-project="selectedProject" />
    </div>
</template>