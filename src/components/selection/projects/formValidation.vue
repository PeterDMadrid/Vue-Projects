<script setup>
import { ref, computed } from 'vue'

const formData = ref({
    name: '',
    email: '',
    password: '',
})

const isNameValid = computed(() => formData.value.name.trim() !== '')
const isEmailValid = computed(() => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value.email))
const isPasswordValid = computed(() => formData.value.password.length >= 8)
const isFormValid = computed(() => isNameValid.value && isEmailValid.value && isPasswordValid.value)

const submitForm = () => {
    if (isFormValid.value) {
        alert('Form is Valid')
        toDisplay.value.name = formData.value.name
        toDisplay.value.email = formData.value.email
        toDisplay.value.password = formData.value.password
    } else {
        alert('Form is not valid')
    }
}

const toDisplay = ref({
    name: '',
    email: '',
    password: ''
})


</script>

<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">Form Validation</h1><br>
        <hr>
        <div>
            <form @submit.prevent="submitForm">
                <div class="flex flex-col">
                    <label for="name">Name:</label>
                    <input v-model="formData.name" class="flex-[1] ml-2 mt-2 p-2 border" type="text">
                    <span v-if="!isNameValid && formData.name">Name is not valid</span>
                </div>
                <div class="flex flex-col">
                    <label for="email">Email:</label>
                    <input v-model="formData.email" class="flex-[1] ml-2 mt-2 p-2 border">
                    <span v-if="!isEmailValid && formData.email">Email is not valid</span>
                </div>
                <div class="flex flex-col">
                    <label for="password">Password:</label>
                    <input v-model="formData.password" class="flex-[1] ml-2 mt-2 p-2 border" type="password">
                    <span v-if="!isPasswordValid && formData.password">Password musst be 8 characters</span>
                </div>
                <button class="border p-2 m-2" type="submit">Submit</button>
            </form>
        </div>
        <div>
            <p>{{ toDisplay.name }}</p>
            <p>{{ toDisplay.email }}</p>
            <p>{{ toDisplay.password }}</p>
        </div>
    </div>
</template>
