<script setup>
import { ref } from 'vue'

const items = ref([
    {
        title: 'Introduction',
        content: 'Welcome to our Vue application. This section gives a brief overview.',
        open: false
    },
    {
        title: 'Features',
        content: 'Our app includes real-time updates, dark mode, and offline support.',
        open: false
    },
    {
        title: 'Contact',
        content: 'Feel free to reach out to us through the contact form on our website.',
        open: false
    }
]);

const toggleAccordiion = (index) => {
    items.value = items.value.map((item, i) => ({
        ...item,
        open: i === index ? !item.open : false
    }))
}


</script>

<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">Accordions Menu</h1><br>
        <hr>
        <div class="flex flex-col mt-4">
            <div class="p-2 bg-blue-100 m-1" v-for="(item, index) in items" :key="index">
                <div class="flex justify-between">
                    <h1 class="font-semibold">{{ item.title }}</h1>
                    <button class="px-2 bg-blue-400 stext-sm cursor-pointer" @click="toggleAccordiion(index)">{{
                        item.open ? "open"
                            : "close" }}</button>
                </div>
                <div class="overflow-hidden transition-all duration-150 ease-in-out"
                    :class="item.open ? 'max-h-96 opacity-100' : 'max-h-0 opacity-0'">
                    <p class="text-sm font-light p-2 pt-0">{{ item.content }}</p>
                </div>
            </div>
        </div>
    </div>
</template>