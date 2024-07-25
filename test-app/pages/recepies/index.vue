<template>
    <div class="bg-zinc-900 min-h-screen">
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 text-white py-20 px-10">
            <div v-for="c in categories" class="relative hover:text-yellow-400 hover:scale-105 duration-300">
                <NuxtLink :to="`/recepies/category/${c.strCategory}`">
                    <img :src="`/images/${c.strCategory.toLowerCase()}.jpg`" class="w-full h-48 object-cover rounded-md">
                    <div class="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center rounded-md hover:bg-opacity-35">
                        <span class="text-xl font-bold uppercase">{{ c.strCategory }}</span>
                    </div>
                </NuxtLink>
            </div>
        </div>
    </div>
</template>


<script setup>
const { data } = await useFetch('https://www.themealdb.com/api/json/v1/1/categories.php')
const categories = data.value.categories || []
</script>
