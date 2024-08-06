<template>
    <div class="bg-zinc-900 min-h-screen">
        <div class="flex justify-center pt-20 ">
            <input
                type="text"
                v-model="searchQuery"
                placeholder="Search for meal"
                class="px-4 py-2 rounded-md bg-zinc-800 text-white placeholder-zinc-500 focus:outline-none focus:ring-2 focus:ring-yellow-400"
                @keyup.enter="performSearch"
            />
            <button
                @click="performSearch"
                class="ml-2 px-4 py-2 bg-yellow-400 rounded-md hover:bg-yellow-300 focus:outline-none focus:ring-2 focus:ring-yellow-500 flex items-center justify-center">
                <Icon name="la:search" class="w-5 h-5" />
            </button>
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 text-white py-7 px-10">
            <div v-for="c in categories" class="relative hover:text-yellow-400 hover:scale-105 duration-300">
                <NuxtLink :to="`/recepies/category/${c.strCategory}`">
                    <img :src="`/images/${c.strCategory.toLowerCase()}.jpg`" class="w-full h-48 object-cover rounded-md">
                    <div class="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center rounded-md hover:bg-opacity-35">
                        <span class="text-xl font-bold uppercase">{{ c.strCategory }}</span>
                    </div>
                </NuxtLink>
            </div>
        </div>
        <hr class="my-1 border-zinc-600 m-8">
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 text-white py-10 px-10">
            <div v-for="a in areas" class="relative hover:text-yellow-400 hover:scale-105 duration-300 m-5">
                <NuxtLink :to="`/recepies/area/${a.strArea}`">
                    <div class="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center rounded-md hover:bg-opacity-35">
                        <span class="text-xl font-bold uppercase">{{ a.strArea }}</span>
                    </div>
                </NuxtLink>
            </div>
        </div>
    </div>
</template>


<script setup>
const { data: data_categories } = await useFetch('https://www.themealdb.com/api/json/v1/1/categories.php')
const categories = data_categories.value.categories || []

const { data : data_areas } = await useFetch("https://www.themealdb.com/api/json/v1/1/list.php?a=list")
const areas = data_areas.value.meals || []

const searchQuery = ref('')
const router = useRouter()
const performSearch = () => {
  if (searchQuery.value) {
    router.push(`/recepies/search/${searchQuery.value}`)
  }
}
</script>
