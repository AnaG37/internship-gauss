<template>
    <footer class="bg-gray-800 text-white text-center pb-7">
        <div class="text-2xl pb-7">
            <a href="#" @click="scrollTop"><Icon name="ri:arrow-up-wide-fill" class="scale-150" style="color: #000;"/></a>
        </div>
      <div class="scroll-smooth flex flex-col md:flex-row items-center">
        <div class="flex flex-col md:flex-row items-center justify-end md:w-1/2 md:pr-10">
          <img src="/public/images/slogan.png" alt="TasteNest Slogan" class="h-20 mb-4 md:mb-0 ">
          <img src="/public/images/logo_bowl.png" alt="TasteNest Logo" class="h-20 mb-4 md:mb-0">
        </div>
        <div class="md:text-left md:w-1/2 md:pl-10">
          <p>Email: <a href="mailto:kontakt@tastenest.com" class="text-blue-300">kontakt@tastenest.com</a></p>
          <p>Phone: <a href="tel:+1234567890" class="text-blue-300">+1234567890</a></p>
          <p>Designed by <a href="https://github.com/AnaG37" target="_blank" rel="noopener noreferrer" class="text-blue-300">Ana</a></p>
        </div>
      </div>
      <div class="pt-6">
        <hr class="my-2 border-gray-600">
        <p>&copy; 2024 TasteNest</p>
      </div>
    </footer>
</template>

<script>
export default {
  methods: {
    scrollTop() {
      window.scrollTo({
        top: 0
      });
    }
  }
};
</script>

<style scoped>
a:hover {
  text-decoration: underline;
}
</style>