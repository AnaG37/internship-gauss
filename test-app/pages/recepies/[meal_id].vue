<template>
    <div v-if="meals.length != 0" class="bg-zinc-900 min-h-screen py-40 md:py-10 px-10 text-white flex flex-col sm:flex-col md:flex-row justify-center md:gap-40">
      <div class="w-full md:w-1/2 md:pr-10 md:pt-20">
        <div class="text-3xl md:text-5xl md:text-3xl font-bold uppercase">{{ meals[0].strMeal }}</div>
        <hr class="my-2 border-customYellow">
        <div class="mt-4">
          <span class="font-bold italic">CATEGORY: </span> {{ meals[0].strCategory }}
        </div>
        <div class="mt-2">
          <span class="font-bold italic">AREA: </span> {{ meals[0].strArea }}
        </div>
        <div class="mt-2">
          <span class="font-bold italic mr-2">INSTRUCTIONS:</span>
          <p class="text-justify">{{ meals[0].strInstructions }}</p>
        </div>
        <div class="mt-2">
          <span class="font-bold italic">Check out Youtube tutorial </span>
          <a :href="meals[0].strYoutube" class="text-blue-300 font-bold italic">here</a>
          <span class="font-bold italic">!</span>
        </div>
        <hr class="my-2 border-customYellow">
        <div class="mt-2">
          <span class="font-bold italic">INGREDIENTS: </span>
          <ol>
            <li v-for="(ingredient, index) in filteredIngredients" :key="index"> {{ index + 1 }}. {{ ingredient }}</li>
          </ol>
        </div>
      </div>
      <div class="relative w-full md:w-1/2 flex justify-center items-center min-h-screen">
        <img src="/public/images/brush_stroke.png" alt="Brush stroke" class="absolute h-full w-96 md:top-10 md:scale-100 scale-75">
        <div class="md:top-36 md:scale-100 scale-75 aspect-w-1 aspect-h-1">
          <img :src="meals[0].strMealThumb" class="relative h-96 w-96 rounded-full mt-20">
        </div>
      </div>
    </div>
</template>
  


<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';
  
const route = useRoute();
const router = useRouter();
const meal_id = ref(route.params.meal_id);
const meals = ref([]);
var filteredIngredients = [];
  
const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${meal_id.value}`);
meals.value = data.value?.meals || [];
  
if (meals.value.length === 0) {
  router.push('/errors/meal-id-not-found');
}
else{
  const ingredients = [];
  for (let i = 1; i <= 20; i++) {
    const strIngredient = "strIngredient" + i;
    ingredients.push(meals.value[0][strIngredient]);
  }
  filteredIngredients = ingredients.filter(ingredient => ingredient !== "");
}
</script>
  