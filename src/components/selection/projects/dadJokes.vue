<script setup>

import { onMounted, ref } from 'vue'

const joke = ref('')

const fetchJoke = async () => {
    try {
        const res = await fetch('https://icanhazdadjoke.com/', {
            headers: { Accept: 'application/json' }
        })
        const data = await res.json();
        joke.value = data.joke
    } catch (e) {
        console.error('Error:', e)
    }
}

</script>

<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">Dad Jokes Generator API</h1><br>
        <hr>
        <div class="flex flex-col m-4">
            <button class="border p-2" @click="fetchJoke">Get Joke</button>
            <p v-if="joke">{{ joke }}</p>
        </div>
    </div>
</template>
