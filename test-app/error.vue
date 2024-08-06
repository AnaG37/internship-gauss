<template>
    <div class="bg-zinc-900 min-h-screen flex flex-col items-center justify-center text-white">
    <h1 class="text-7xl font-bold text-center">{{ error.statusCode }}</h1>
    <p class="text-center mt-4">
        {{ error.message }}
    </p>
    <div class="text-center mt-6">
      <NuxtLink to="/" class="text-red-700 hover:text-white font-semibold px-4 py-2 border border-red-700 rounded-md hover:bg-red-700 transition-colors duration-300"
        >Go Home</NuxtLink>
    </div>
  </div>
</template>
  
<script setup>
  const props = defineProps(["error"]);
</script>