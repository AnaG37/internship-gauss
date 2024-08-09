<script setup lang="ts">
import Header from '~/components/header.vue';
import Footer from '~/components/footer.vue';
</script>

<template>
    <div class="min-h-screen flex flex-col bg-zinc-900 text-white">
      <Header />
      <main class="flex-grow min-h-screen">
        <NuxtPage />
      </main>
      <Footer />
    </div>
</template>