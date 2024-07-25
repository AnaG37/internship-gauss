<template>
    <div class="bg-zinc-900 min-h-screen text-white grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 py-20 px-10">
      <div v-for="m in meals" :key="m.idMeal" class="relative bg-zinc-950 bg-opacity-75 rounded-md shadow-lg overflow-hidden flex flex-col transition-transform duration-300 hover:scale-105 hover:text-yellow-400">
        <NuxtLink :to="`/recepies/${m.idMeal}`" class="block h-full flex flex-col">
          <div class="relative flex-1 overflow-hidden">
            <img :src="`${m.strMealThumb}`" class="w-full h-48 object-cover transition-transform duration-300 hover:scale-110 opacity-75" />
          </div>
          <div class="p-4 text-center flex-shrink-0">
            <div class="text-lg md:text-xl font-bold uppercase">{{ m.strMeal }}</div>
          </div>
        </NuxtLink>
      </div>
    </div>
</template>

<script setup>
const route = useRoute();
const categoryName = ref(route.params.category_name);
const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/filter.php?c=${categoryName.value}`)
const meals = data.value.meals || []
console.log(data)
</script>