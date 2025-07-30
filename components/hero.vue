<script setup>
import { marked } from 'marked';
const URLIMAGES = useRuntimeConfig().public.ApiURL;
const { data: Contents, error } = await useFetch(
  `${URLIMAGES}/api/home-page`,
  {
    query: { populate: 'image' },
    transform: res => res.data
  }

);
</script>
<template>
    <main class="relative mt-10 md:mt-28 px-5 md:px-17">
      <img :src="URLIMAGES + Contents.image.url" :alt="Contents"  loading="lazy" class="border-1 w-[100%] h-[70vh] md:h-[80vh] object-cover brightness-[70%]">
      <div class="flex justify-center align-center">
        <img src="/public/icon/LogoWasted.png" alt="Wasted" loading="lazy" class="absolute top-[140px] w-[100px] md:w-[170px]">
      </div>
      <div class="flex justify-center align-center">
        <h1 class="absolute top-[300px] md:top-[390px] ExposureTrialVARBold text-[#ece6da] text-[14px] md:text-[20px] text-center w-[240px] md:w-[500px] lg:w-[700px]">{{ Contents.HeroText }}</h1>
      </div>
    </main>
    <div class="flex justify-center align-center px-6 mt-16">
      <h4 v-html="marked(Contents.description)" class="text-left md:text-center text-[14px] w-[730px] GeistMono"></h4>
    </div>
</template>