<template>
    <ListOfMeals :meals="meals" />
</template>

<script setup>
const route = useRoute();
const categoryName = ref(route.params.category_name);
const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/filter.php?c=${categoryName.value}`)
const meals = data.value.meals || []
console.log(data)
</script>