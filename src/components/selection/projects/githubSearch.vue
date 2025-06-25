<script setup>
import { onMounted, ref } from 'vue'

const username = ref('PeterDMadrid')
const userProfilePicture = ref('')
const error = ref(null)

const getUserProfile = async () => {
    try {
        const response = await fetch(`https://api.github.com/users/${username.value}`)
        const data = await response.json()

        userProfilePicture.value = data.avatar_url
        console.log(data)
    } catch (e) {
        console.error('Error fetching data:', e)
        error.value = e
    }
}

</script>

<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">Github Search</h1><br>
        <hr>
        <div class="mt-4">
            <form @submit.prevent="getUserProfile">
                <input v-model="username" type="text" class="border p-2 my-4">
                <button type="submit" class="my-2 p-2 border">Search</button>
            </form>
            <img :src="userProfilePicture" alt="">
        </div>
    </div>
</template>
