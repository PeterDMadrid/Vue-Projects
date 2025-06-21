<script setup>
import { computed } from 'vue'
import toDoApp from '../selection/projects/toDoApp.vue';
import randomQuoteGenerator from '../selection/projects/randomQuoteGenerator.vue';
import noobCalculator from '../selection/projects/noobCalculator.vue'
import accordionsMenu from '../selection/projects/accordionsMenu.vue';
import formValidation from '../selection/projects/formValidation.vue';
import passwordGenerator from '../selection/projects/passwordGenerator.vue';

const props = defineProps(['selectedProject'])

const currentComponent = computed(() => {
    switch (props.selectedProject) {
        case 'To Do App':
            return toDoApp
        case 'Random Quote Generator':
            return randomQuoteGenerator
        case 'Noob Calculator':
            return noobCalculator
        case 'Accordions Menu':
            return accordionsMenu
        case 'Form Validation':
            return formValidation
        case 'Password Generator':
            return passwordGenerator
        default:
            return null
    }
})
</script>

<template>
    <div class="border p-4 m-4 bg-white rounded-lg shadow-md w-full h-136 overflow-y-auto">
        <h1 class="text-xl font-bold mb-4">Display Project</h1>

        <div v-if="selectedProject" class="mb-4">
            <p class="text-sm text-gray-600">Selected: <span class="font-medium">{{ selectedProject }}</span></p>
        </div>

        <div v-if="currentComponent" class="border-t pt-4">
            <component :is="currentComponent" />
        </div>

        <div v-else-if="selectedProject" class="text-gray-500 italic">
            Component for "{{ selectedProject }}" not implemented yet
        </div>

        <div v-else class="text-gray-400 italic">
            Select a project from the left to display it here
        </div>
    </div>
</template>