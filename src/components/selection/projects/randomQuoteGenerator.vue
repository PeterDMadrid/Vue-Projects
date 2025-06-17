<script setup>
import { ref, onMounted } from 'vue'

const isLoading = ref(false)

const currentQuote = ref({ quote: '', author: '' })

const getRandomQuote = async () => {
    isLoading.value = true
    try {
        try {
            const res = await fetch('https://api.api-ninjas.com/v1/quotes', {
                headers: {
                    'X-Api-Key': 'SZu+kY0GrsD9VTxfJkVtzw==rpAKBrQ4U7obzTpe'
                }
            });
            const data = await res.json();
            currentQuote.value = data[0]
        } catch (error) {
            console.error('Error fetching quote:', error);
        }
    } finally {
        isLoading.value = false
    }

}


onMounted(getRandomQuote)


</script>

<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">Quote Generator</h1><br>
        <hr>
        <div class="flex flex-col justify-center items-center border h-44 mt-12 p-4" v-if="!isLoading">
            <h2 class="text-sm font-thin mt-4">{{ currentQuote.quote }}</h2>
            <h3 class="font-semibold">{{ currentQuote.author }}</h3>
            <button @click="getRandomQuote" class="border m-4 p-1 cursor-pointer">More!</button>
        </div>
        <div class="flex flex-col justify-center items-center border h-44 mt-12 p-4" v-if="isLoading">
            Loading Quote
        </div>
    </div>
</template>