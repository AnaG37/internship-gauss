<template>
    <div class="bg-black">
        <nav>
            <ul class="md:hidden p-4 text-white md:min-h-fit">
                <li @click="showMenu = !showMenu">
                    <Icon name="simple-line-icons:menu" color="white" />
                </li>
            </ul>
            <ul class="flex  md:flex-row flex-col md:space-x-12 space-x-0 p-4 text-white justify-end bg-black min-h-[25vh] gap-3 md:min-h-fit " v-if="showMenu">
                <li class="hover:text-gray-500"><NuxtLink to="/">Home</NuxtLink></li>
                <li class="hover:text-gray-500"><NuxtLink to="/recepies">Recepies</NuxtLink></li>
                <li class="hover:text-gray-500"><NuxtLink to="/favorites">Favorites</NuxtLink></li>
                <li class="pr-10 hover:text-gray-500"><NuxtLink to="/about-us">About us</NuxtLink></li>
            </ul>
        </nav>
    </div>
</template>

<script>
  export default {
  data() {
    return {
      showMenu: false
    };
  }
};
</script>
