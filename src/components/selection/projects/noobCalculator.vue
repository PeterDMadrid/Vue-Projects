<script setup>
import { ref, computed } from 'vue'
const buttons = [
    ['1', '2', '3', '/'],
    ['4', '5', '6', '*'],
    ['7', '8', '9', '+'],
    ['0', '.', '=', '-'],
]

const display = ref('0')

const toDisplay = (value) => {
    if (display.value === '0' && value !== '.') {
        display.value = value
    } else {
        display.value = display.value + value
    }
}

const calculate = () => {
    try {
        display.value = eval(display.value).toString()
    } catch {
        display.value = 'Error'
    }
}

const clear = () => {
    display.value = '0'
}


const handleClick = (button) => {
    if (button === '=') {
        calculate()
    } else {
        toDisplay(button)
    }
}
</script>

<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">Noob Calculator</h1><br>
        <hr>
        <div class="mt-4 h-64 p-4 border">
            <div class="flex flex-row">
                <input v-model="display" class="flex items-center justify-end border mr-2 flex-[3] bg-white pl-4"
                    readonly />
                <button @click="clear"
                    class="flex justify-center items-center border flex-1 bg-black text-white cursor-pointer">C</button>
            </div>
            <div v-for="(row, rowIndex) in buttons" :key="rowIndex" class="mt-2 flex">
                <button v-for="(button, buttonIndex) in row" :key="buttonIndex"
                    :class="buttonIndex < row.length - 1 ? 'mr-2' : ''" @click="handleClick(button)"
                    class="border p-2 flex-1 bg-black text-white cursor-pointer">
                    {{ button }}
                </button>
            </div>
        </div>
    </div>
</template>
