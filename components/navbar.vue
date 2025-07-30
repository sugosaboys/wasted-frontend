<script setup>
import { ref } from 'vue'

const showUp = ref(false);
</script>

<template>
  <nav class="flex flex-col md:flex-row justify-between items-center px-[30px] md:px-[68px] py-3 fixed top-0 left-0 right-0 z-50 bg-[#ece6da] md:bg-transparent">
    <div class="flex justify-between items-center w-full md:w-auto">
      <nuxt-link to="/">
        <img src="/public/icon/WastedLogo.svg" alt="Wasted Logo" class="w-[33px] md:w-[44px] md:h-[50px]" loading="lazy" />
      </nuxt-link>
      <img
        :src="showUp ? '/icon/xbtn.svg' : '/icon/hamburger.svg'"
        alt="menu icon"
        loading="lazy"
        class="block md:hidden w-4 cursor-pointer"
        @click="showUp = !showUp"
      />
    </div>
    <ul
      :class="[
        'transition-opacity duration-300 ease-in-out',
        'absolute md:relative left-0 top-[60px] md:top-0 flex flex-col md:flex-row gap-8 bg-[#ece6da] md:bg-transparent w-full md:w-auto h-[200vh] md:h-auto text-[#241f21] ExposureTrialVAR font-black text-[15px] pt-10 md:pt-0 px-10 md:px-0 md:mt-4',
        showUp ? 'opacity-100 pointer-events-auto' : 'opacity-0 pointer-events-none md:opacity-100 md:pointer-events-auto'
      ]"
    >
      <nuxt-link to="/about">
        <li class="hoverNav hover:text-[#0d7dbb] h-5 cursor-pointer">About</li>
      </nuxt-link>
      <nuxt-link to="/products">
        <li class="hoverNav hover:text-[#0d7dbb] h-5 cursor-pointer">Collection 001</li>
      </nuxt-link>
      <nuxt-link to="https://shop.potatohead.co/">
        <li class="flex items-center hoverNav hover:text-[#0d7dbb] cursor-pointer group h-5">
          Shop
          <img src="/icon/Arrowup-right.svg" alt="arrow" class="w-[12px] h-[12px] mt-1 ml-1 block group-hover:hidden" loading="lazy" />
          <img src="/icon/Arrowup-right-blue.svg" alt="arrow hover" class="w-[12px] h-[12px] mt-1 ml-1 hidden group-hover:block" loading="lazy" />
        </li>
      </nuxt-link>
    </ul>
  </nav>
</template>
