<template>
  <div  v-if="meals.length !== 0">
    <div class="flex justify-center pt-20 bg-zinc-900">
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
      <ListOfMeals class="-mt-10" :meals="meals" />
  </div>
    
    <div v-else class="min-h-screen bg-zinc-900 flex flex-col justify-center items-center text-white">
      <h1 class="text-4xl font-bold text-center">
        No meals found for "{{ search_value }}"!
      </h1>
      <p class="text-center mt-4">
        The meal you are looking for does not exist.
      </p>
      <div class="text-center mt-6">
        <NuxtLink to="/recepies" class="text-red-700 hover:text-white font-semibold px-4 py-2 border border-red-700 rounded-md hover:bg-red-700 transition-colors duration-300">
          Go Back
        </NuxtLink>
      </div>
    </div>
  </template>

<script setup>
const route = useRoute();
const router = useRouter()
const searchQuery = ref('')

const search_value = ref(route.params.search_value);
const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/search.php?s=${search_value.value}`)
const meals = data.value.meals || []

const performSearch = () => {
  if (searchQuery.value) {
    router.push(`/recepies/search/${searchQuery.value}`)
  }
}
</script>