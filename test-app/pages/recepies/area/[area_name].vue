<template>
  <ListOfMeals :meals="meals" />
</template>

<script setup>
const route = useRoute();
const areaName = ref(route.params.area_name);
const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/filter.php?a=${areaName.value}`)
const meals = data.value.meals || []
console.log(data)
</script>