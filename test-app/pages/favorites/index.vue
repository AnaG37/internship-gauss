<template>
  <div class="bg-zinc-900">
    <div class="text-4xl font-bold text-center text-yellow-400 pb-4 pt-20">
      Your Favorite Meals
    </div>
    <hr class="border-customYellow mx-10">
    <div v-if="loading" class="absolute inset-0 flex flex-col justify-center items-center">
      <Icon name="eos-icons:bubble-loading" class="text-customYellow text-5xl mb-5"/>
      <div class="text-lg">Loading...</div>
    </div>
    <ListOfMeals v-if="!loading && meals.length !== 0" :meals="meals" />
    <div v-if="!loading && meals.length === 0" class="text-center text-gray-400 mt-10">
      No favorite meals found. Add some meals to your favorites!
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const meals = ref([]);
const loading = ref(true);

onMounted(async () => {

const favoriteMealIDs = [];
for (let i = 0; i < localStorage.length; i++) {
  const key = localStorage.key(i);
  const value = localStorage.getItem(key);

  if (!isNaN(key) && value === 'true') {
    favoriteMealIDs.push(key);
  }
}

const apiCalls = favoriteMealIDs.map(mealId => {
  return fetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${mealId}`)
    .then(response => response.json())
    .then(data => data.meals[0]); 
});

meals.value = await Promise.all(apiCalls);
loading.value = false;
});
</script>
