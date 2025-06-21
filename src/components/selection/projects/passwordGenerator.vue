<script setup>

import { ref, computed, watch, reactive } from 'vue'

const passwordLength = ref(8)

const choices = reactive({
    isLowerActive: false,
    isUpperActive: false,
    isSpecialActive: false,
    isNumberActive: false
})

watch(() => choices.isLowerActive, (newVal, oldVal) => {
    console.log(newVal)
    if (newVal) {
        characters.value.lowerCases = "abcdefghijklmnopqrstuvwxyz"
    } else {
        characters.value.lowerCases = ""
    }

    console.log(characters.value.lowerCases)
})

watch(() => choices.isUpperActive, (newVal, oldVal) => {
    if (newVal) {
        characters.value.upperCases = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    } else {
        characters.value.upperCases = ""
    }
})


watch(() => choices.isSpecialActive, (newVal, oldVal) => {
    if (newVal) {
        characters.value.specials = "!@#$%^&*()_+-=[]{}|;:',.<>?/"
    } else {
        characters.value.specials = ""
    }
})

watch(() => choices.isNumberActive, (newVal, oldVal) => {
    if (newVal) {
        characters.value.numbers = "0123456789"
    } else {
        characters.value.numbers = ""
    }
})


const hasValidSelection = computed(() => {
    const activeCount = [
        choices.isLowerActive,
        choices.isUpperActive,
        choices.isSpecialActive,
        choices.isNumberActive
    ].filter(Boolean).length

    return activeCount >= 2
})

const generatedPassword = ref('')

const characters = ref({
    lowerCases: "",
    upperCases: "",
    numbers: "",
    specials: ""
})

const allCharacters = computed(() => {
    return characters.value.lowerCases + characters.value.upperCases + characters.value.numbers + characters.value.specials
})

const generatePassword = () => {

    let password = '';
    for (let i = 0; i < passwordLength.value; i++) {
        const randomIndex = Math.floor(Math.random() * allCharacters.value.length)
        password = password + allCharacters.value[randomIndex]
    }
    generatedPassword.value = password
}



</script>

<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">Password Generator</h1><br>
        <hr>
    </div>
    <div class="flex flex-col mt-2">
        <form>
            <div class="flex flex-col items-start">

                <div>
                    <input type="checkbox" v-model="choices.isLowerActive">
                    <label for="lowerCase" class="ml-2">Lower Case</label>
                </div>

                <div>
                    <input type="checkbox" v-model="choices.isUpperActive">
                    <label for="upperCase" class="ml-2">Upper Case</label>
                </div>

                <div>
                    <input type="checkbox" v-model="choices.isSpecialActive">
                    <label for="upperCase" class="ml-2">Special Characters</label>
                </div>

                <div>
                    <input type="checkbox" v-model="choices.isNumberActive">
                    <label for="upperCase" class="ml-2">Number Characters</label>
                </div>

                <label for="length">Enter Password length</label>
                <input type="text" v-model="passwordLength" class="p-1 border my-2">
            </div>
        </form>
        <button @click="generatePassword" :class="!hasValidSelection ? 'text-red-600' : 'text-green-600'"
            :disabled="!hasValidSelection" class="p-2 border cursor-pointer">
            {{ !hasValidSelection ? 'Must check atleast 2' : 'Generate' }}</button>
        <p>Your password: {{ generatedPassword }}</p>
        <p>Password length: {{ passwordLength }}</p>
    </div>
</template>