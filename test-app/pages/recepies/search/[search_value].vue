<template>
    <ListOfMeals v-if="meals.length !== 0" :meals="meals" />
    <div v-else class="min-h-screen bg-zinc-900 flex flex-col justify-center items-center text-white">
      <h1 class="text-4xl font-bold text-center">
        No meals found for "{{ search_value }}"!
      </h1>
      <div class="text-center mt-6">
        <NuxtLink to="/recepies" class="text-red-700 hover:text-white font-semibold px-4 py-2 border border-red-700 rounded-md hover:bg-red-700 transition-colors duration-300">
          Go Back
        </NuxtLink>
      </div>
    </div>
  </template>

<script setup>
const route = useRoute();
const search_value = ref(route.params.search_value);
const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/search.php?s=${search_value.value}`)
const meals = data.value.meals || []
console.log(data)
</script>