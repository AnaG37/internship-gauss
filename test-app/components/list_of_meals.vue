<template>
    <div class="bg-zinc-900 min-h-screen text-white grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-4 gap-6 py-20 px-10">
        <div v-for="m in meals" :key="m.idMeal" class="overflow-hidden max-h-72 relative bg-zinc-950 bg-opacity-75 rounded-md shadow-lg flex flex-col transition-transform duration-300 hover:scale-105 hover:text-yellow-400">
          <NuxtLink :to="`/recepies/${m.idMeal}`" class="flex flex-col flex-1">
            <div class="relative flex-1">
              <img :src="`${m.strMealThumb}`" class="w-full h-48 object-cover transition-transform duration-300 hover:scale-110 opacity-75" />
            </div>
            <div class="p-4 text-center">
              <div class="text-lg md:text-xl font-bold uppercase">{{ m.strMeal }}</div>
            </div>
          </NuxtLink>
        </div>
      </div>
</template>

<script setup>
defineProps({
  meals: {
    type: Array,
    required: true
  }
});
</script>