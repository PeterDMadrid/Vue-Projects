<template>
    <div class="p-4 bg-blue-50 rounded">
        <h1 class="text-2xl font-bold text-blue-800">Noob Calculator</h1><br>
        <hr>
        <div class="mt-4 h-64 p-4 border">
            <div class="flex flex-row">
                <div class="flex items-center justify-end border mr-2 flex-[3] bg-white"></div>
                <button
                    class="flex justify-center items-center border flex-1 bg-black text-white cursor-pointer">C</button>
            </div>
            <div class="mt-2 flex">
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">1</button>
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">2</button>
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">3</button>
                <button class="border p-2 flex-1 bg-black text-white cursor-pointer">/</button>
            </div>
            <div class="mt-2 flex">
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">4</button>
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">5</button>
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">6</button>
                <button class="border p-2 flex-1 bg-black text-white cursor-pointer">*</button>
            </div>
            <div class="mt-2 flex">
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">7</button>
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">8</button>
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">9</button>
                <button class="border p-2 flex-1 bg-black text-white cursor-pointer">+</button>
            </div>
            <div class="mt-2 flex">
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">0</button>
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">.</button>
                <button class="border p-2 flex-1 mr-2 bg-black text-white cursor-pointer">=</button>
                <button class="border p-2 flex-1 bg-black text-white cursor-pointer">-</button>
            </div>
        </div>
    </div>
</template>