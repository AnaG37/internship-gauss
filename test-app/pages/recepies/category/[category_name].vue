<template>
    <ListOfMeals v-if="meals.length != 0" :meals="meals" />
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();
const meals = ref([]);
const categoryName = ref(route.params.category_name);

const { data } = await useFetch(`https://www.themealdb.com/api/json/v1/1/filter.php?c=${categoryName.value}`)
meals.value = data.value?.meals || []

if (meals.value.length === 0) {
  router.push('/errors/category-name-not-found');
}

</script>