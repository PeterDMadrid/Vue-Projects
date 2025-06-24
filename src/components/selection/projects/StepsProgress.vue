<script setup>

import { ref } from 'vue'

const steps = ref(['Step 1', 'Step 2', 'Step 3'])
const isDisabled = ref(false)
const currentIndex = ref(0)

const nextStep = () => {
    if (currentIndex.value < steps.value.length - 1) {//0:3 1:3 2:3 3:3
        currentIndex.value++
        console.log("next")
    } else {
        isDisabled = true
    }
}

const prevStep = () => {
    if (currentIndex.value !== 0) {
        currentIndex.value--
        console.log("prev")
    } else {
        isDisabled = true
    }
}

</script>

<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">Steps Progress</h1><br>
        <hr>
        <div>
            <div class="flex">
                <div :class="(currentIndex == index ? 'flex-3' : 'flex-1')"
                    class="p-2 m-1 border  transition-all duration-300 ease-in-out" v-for="(step, index) in steps"
                    :key="index">{{ step }}</div>
            </div>
            <div>
                <p>{{ steps[currentIndex] }}</p>
                <button :disabled="isDisabled" class="p-2 m-1 border cursor-pointer" @click="prevStep">Prev</button>
                <button :disabled="isDisabled" class="p-2 m-1 border cursor-pointer" @click="nextStep">Next</button>
            </div>

        </div>
    </div>

</template>