<template>
  <div class="bg-zinc-900 min-h-screen flex flex-col justify-center items-center text-white">
    <h1 class="text-4xl font-bold text-center">Meal ID Not Found</h1>
    <p class="text-center mt-4">
      The meal ID you are looking for does not exist.
    </p>
    <div class="text-center mt-6">
      <NuxtLink to="/" class="text-red-700 hover:text-white font-semibold px-4 py-2 border border-red-700 rounded-md hover:bg-red-700 transition-colors duration-300"
        >Go Home</NuxtLink>
    </div>
  </div>
</template>

<script></script>