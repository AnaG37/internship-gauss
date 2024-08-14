<template>
    <div v-if="meals.length != 0" class="bg-zinc-900 min-h-screen py-40 md:py-10 px-10 text-white flex flex-col sm:flex-col md:flex-row justify-center md:gap-40">
      <div class="w-full md:w-1/2 md:pr-10 md:pt-20">
        <div class="text-3xl md:text-5xl font-bold uppercase flex items-center ">
          {{ meals[0].strMeal }}
          <Icon name="ph:heart-duotone" 
                :class="{
                  'pl-20 w-9 h-9 hover:scale-110 transition-colors duration-300 cursor-pointer': true,
                  'text-red-500': isClicked,
                  'text-gray-500': !isClicked
                }"
                @click="toggleClick"
                />
        </div>
        <hr class="my-2 border-customYellow">
        <div class="mt-4 text-lg">
          <span class="font-bold italic text-yellow-400">CATEGORY: </span> {{ meals[0].strCategory }}
        </div>
        <div class="mt-2 text-lg">
          <span class="font-bold italic text-yellow-400">AREA: </span> {{ meals[0].strArea }}
        </div>
        <div class="mt-2 text-lg">
          <span class="font-bold italic mr-2 text-yellow-400">INSTRUCTIONS:</span>
          <p class="text-justify">{{ meals[0].strInstructions }}</p>
        </div>
        <div class="mt-7">
          <span class="font-bold italic">Check out Youtube tutorial </span>
          <a :href="meals[0].strYoutube" class="text-blue-300 font-bold italic">here</a>
          <span class="font-bold italic">!</span>
        </div>
        <hr class="my-2 border-customYellow">
        <table class="table-auto w-full border-collapse border border-gray-700 mt-5">
          <thead>
            <tr class="bg-gray-800 text-yellow-400">
              <th class="font-bold italic py-2 px-4 border-b border-gray-600">#</th>
              <th class="font-bold italic py-2 px-4 border-b border-gray-600">INGREDIENTS:</th>
              <th class="font-bold italic py-2 px-4 border-b border-gray-600">MEASURE:</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in filteredIngredients" :key="index" class="border-b border-gray-600 text-center">
              <td class="py-2 px-4">{{ index + 1 }}.</td>
              <td class="py-2 px-4">{{ item.ingredient }}</td>
              <td class="py-2 px-4">{{ item.measure }}</td>
            </tr>
          </tbody>
      </table>
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
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';

const route = useRoute();
const router = useRouter();
const meal_id = ref(route.params.meal_id);
const meals = ref([]);
var filteredIngredients = [];
const isClicked = ref(false);
  
const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${meal_id.value}`);
meals.value = data.value?.meals || [];
  
if (meals.value.length === 0) {
  router.push('/errors/meal-id-not-found');
}
else{
  const ingredients = [];
  const measures = [];

  let i = 1;
  while (meals.value[0]['strIngredient' + i]) {
    const strIngredient = 'strIngredient' + i;
    const strMeasure = 'strMeasure' + i;

    ingredients.push(meals.value[0][strIngredient]);
    measures.push(meals.value[0][strMeasure]);

    i++;
    console.log(meals.value[0]['strIngredient' + i]);
  }

  filteredIngredients = ingredients
    .map((ingredient, index) => ingredient !== "" ? { ingredient, measure: measures[index] } : null)
    .filter(item => item !== null);
}

onMounted(() => {
  if (localStorage.getItem(meal_id.value) === 'true') {
    isClicked.value = true;
  }
});

function toggleClick() {
  isClicked.value = !isClicked.value;
  if (isClicked.value) {
    localStorage.setItem(meal_id.value, 'true');
    toast.success('Added to favorites!',
      {autoClose: 2000,
        position: 'bottom-right',
        transition: 'bounce',
      }
    )
  }
  else{
    localStorage.removeItem(meal_id.value)
  }
}
</script>
  