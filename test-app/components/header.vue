<template>
    <div class="bg-black fixed w-full z-10">
        <nav>
            <ul class="md:hidden p-4 pl-8 text-white md:min-h-fit">
                <li @click="showMenu = !showMenu" class="flex flex-row items-center justify-between">
                    <Icon name="simple-line-icons:menu" color="white" />
                    <div class="flex items-center space-x-3">
                      <img src="/public/images/ime.png" alt="TasteNest Name" class="h-5">
                      <img src="/public/images/logo_bowl.png" alt="TasteNest Logo" class="h-7">
                    </div>
                </li>
            </ul>
            <transition name="bounce">
            <ul class="hidden md:flex flex-row space-x-12 pt-4 text-gray-300 bg-black min-h-[20vh] min-h-fit text-center pb-2" v-if="isMediumOrLarger">
                <div class="md:flex items-center mr-auto space-x-3 hidden pl-10">
                  <img src="/public/images/logo_bowl.png" alt="TasteNest Logo"  class="h-7">
                  <img src="/public/images/ime.png" alt="TasteNest Name"  class="h-5">
                </div>
                <li class="hover:text-white transition ease-in-out delay-100 hover:-translate-y-1 hover:scale-105 duration-200"><NuxtLink to="/">Home</NuxtLink></li>
                <li class="hover:text-white transition ease-in-out delay-100 hover:-translate-y-1 hover:scale-105 duration-200"><NuxtLink to="/recepies">Recepies</NuxtLink></li>
                <li class="hover:text-white transition ease-in-out delay-100 hover:-translate-y-1 hover:scale-105 duration-200"><NuxtLink to="/favorites">Favorites</NuxtLink></li>
                <li class="pr-10 hover:text-white transition ease-in-out delay-100 hover:-translate-y-1 hover:scale-105 duration-200"><NuxtLink to="/about-us">About us</NuxtLink></li>
            </ul>
          </transition>
          <transition name="bounce">
            <sidebar class="md:hidden" v-if="showMenu"></sidebar>
          </transition>
        </nav>
    </div>
</template>

<script>
export default {
  data() {
    return {
      showMenu: false,
      isMediumOrLarger: false
    };
  },
  mounted() {
    this.checkScreenSize();
    window.addEventListener('resize', this.checkScreenSize);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.checkScreenSize);
  },
  methods: {
    toggleMenu() {
      this.showMenu = !this.showMenu;
    },
    checkScreenSize() {
      this.isMediumOrLarger = window.innerWidth >= 768;
    }
  }
};
</script>

<style>
@keyframes bounceIn {
  0% {
    opacity: 0;
    transform: scale(0.95);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes bounceOut {
  0% {
    opacity: 1;
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    opacity: 0;
    transform: scale(0.95);
  }
}

.bounce-enter-active {
  animation: bounceIn 0.4s;
}
.bounce-leave-active {
  animation: bounceOut 0.4s;
}
</style>
