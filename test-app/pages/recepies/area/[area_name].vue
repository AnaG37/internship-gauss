<template>
  <ListOfMeals v-if="meals.length != 0" :meals="meals" />
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();
const meals = ref([]);
const areaName = ref(route.params.area_name);

const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/filter.php?a=${areaName.value}`)
meals.value = data.value?.meals || []

if (meals.value.length === 0) {
  router.push('/errors/area-name-not-found');
}
</script>