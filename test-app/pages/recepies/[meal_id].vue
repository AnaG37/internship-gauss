<template>
    <div class="bg-zinc-900 min-h-screen py-10 px-10 text-white relative">
        <img src="/public/images/brush_stroke.png" alt="Brush stroke" class="absolute right-0 h-5/6 w-96 right-20">
        <div class="absolute right-20 top-36 flex justify-center items-center">
            <img :src="meals[0].strMealThumb" class="h-96 w-96 object-cover rounded-full">
        </div>
  
        <div class="absolute top-20 left-10 w-1/2">
            <div class="text-5xl md:text-3xl font-bold uppercase">{{ meals[0].strMeal }}</div>
            <hr class="my-2 border-zinc-600">
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
                <span class="font-bold italic">YOUTUBE: </span> 
                <a :href="meals[0].strYoutube" class="text-blue-300">{{ meals[0].strYoutube }}</a>
            </div>
            <hr class="my-2 border-zinc-600">
            <div class="mt-2">
                <span class="font-bold italic">INDGRIDIENTS: </span> 
            </div>
        </div>
    </div>
</template>
  
  
<script setup>
const route = useRoute();
const meal_id = ref(route.params.meal_id);
const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${meal_id.value}`)
const meals = data.value.meals || []
console.log(meals)
</script>