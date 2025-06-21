<script setup>
import { ref, computed } from 'vue'

const formData = ref({
    name: '',
    email: '',
    password: '',
})

const submittedData = ref({
    name: '',
    email: '',
    password: ''
})

const validationRules = {
    name: (value) => value.trim().length > 0,
    email: (value) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value),
    password: (value) => value.length >= 8
}

const validation = computed(() => ({
    name: {
        isValid: validationRules.name(formData.value.name),
        message: 'Name is required'
    },
    email: {
        isValid: validationRules.email(formData.value.email),
        message: 'Please enter a valid email address'
    },
    password: {
        isValid: validationRules.password(formData.value.password),
        message: 'Password must be at least 8 characters'
    }
}))

const isFormValid = computed(() =>
    Object.values(validation.value).every(field => field.isValid)
)

const submitForm = () => {
    if (isFormValid.value) {
        Object.assign(submittedData.value, formData.value)
        alert('Form submitted successfully!')
    } else {
        alert('Please fix the errors before submitting')
    }
}

const shouldShowError = (fieldName) =>
    formData.value[fieldName] && !validation.value[fieldName].isValid

const formFields = [
    { name: 'name', label: 'Name', type: 'text' },
    { name: 'email', label: 'Email', type: 'email' },
    { name: 'password', label: 'Password', type: 'password' }
]
</script>

<template>
    <div class="p-6 bg-blue-50 rounded-lg">
        <h1 class="text-2xl font-bold text-blue-800 mb-4">Form Validation</h1>
        <hr class="mb-6">

        <form @submit.prevent="submitForm" class="space-y-4">
            <div v-for="field in formFields" :key="field.name" class="flex flex-col space-y-2">
                <label :for="field.name" class="font-medium text-gray-700">
                    {{ field.label }}:
                </label>

                <input :id="field.name" v-model="formData[field.name]" :type="field.type"
                    class="p-3 border rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    :class="shouldShowError(field.name) ? 'border-red-500' : 'border-gray-300'">

                <span v-if="shouldShowError(field.name)" class="text-red-500 text-sm">
                    {{ validation[field.name].message }}
                </span>
            </div>

            <button type="submit"
                class="px-6 py-3 bg-blue-600 text-white rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-colors"
                :class="isFormValid ? 'cursor-pointer' : 'opacity-50 cursor-not-allowed'">
                Submit
            </button>
        </form>

        <div v-if="submittedData.name || submittedData.email || submittedData.password"
            class="mt-8 p-4 bg-green-50 border border-green-200 rounded-lg">
            <h3 class="font-semibold text-green-800 mb-3">Submitted Data:</h3>
            <div class="space-y-2 text-sm">
                <p><strong>Name:</strong> {{ submittedData.name }}</p>
                <p><strong>Email:</strong> {{ submittedData.email }}</p>
                <p><strong>Password:</strong> {{ '*'.repeat(submittedData.password.length) }}</p>
            </div>
        </div>

        <div class="mt-6 p-4 bg-gray-100 rounded-lg">
            <h4 class="font-medium text-gray-700 mb-2">Form Status:</h4>
            <p class="text-sm">
                <strong>Valid:</strong>
                <span :class="isFormValid ? 'text-green-600' : 'text-red-600'">
                    {{ isFormValid ? 'Yes' : 'No' }}
                </span>
            </p>
        </div>
    </div>
</template>
