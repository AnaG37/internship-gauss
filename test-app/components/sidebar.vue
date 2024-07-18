<template>
    <div class="bg-black fixed w-full z-10">
        <nav>
            <ul class="flex flex-col pl-8 pb-4 text-gray-300 bg-black min-h-[20vh] gap-3">
                <li class="hover:text-white transition ease-in-out delay-100 hover:-translate-y-1 hover:scale-105 duration-200"><NuxtLink to="/">Home</NuxtLink></li>
                <li class="hover:text-white transition ease-in-out delay-100 hover:-translate-y-1 hover:scale-105 duration-200"><NuxtLink to="/recepies">Recepies</NuxtLink></li>
                <li class="hover:text-white transition ease-in-out delay-100 hover:-translate-y-1 hover:scale-105 duration-200"><NuxtLink to="/favorites">Favorites</NuxtLink></li>
                <li class="pr-10 hover:text-white transition ease-in-out delay-100 hover:-translate-y-1 hover:scale-105 duration-200"><NuxtLink to="/about-us">About us</NuxtLink></li>
            </ul>
        </nav>
    </div>
</template>
