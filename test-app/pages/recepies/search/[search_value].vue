<template>
    <ListOfMeals :meals="meals" />
</template>

<script setup>
const route = useRoute();
const search_value = ref(route.params.search_value);
const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/search.php?s=${search_value.value}`)
const meals = data.value.meals || []
console.log(data)
</script>