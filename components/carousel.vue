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

const activeIndex = ref(0)

onMounted(() => {
  const interval = setInterval(() => {
    activeIndex.value++
  }, 5000)

  onBeforeUnmount(() => {
    clearInterval(interval)
  })
});
</script>
<template>
    <main class="relative flex justify-center align-center pt-35 px-8 md:px-0">
        <div class="relative lg:flex lg:justify-center lg:align-center lg:gap-8 w-[420px] md:w-[720px] lg:w-full">
            <div v-for="(content,index) in Contents.image" :key="index" :class="{'transition-all ease-in-out duration-500 opacity-100 z-10': index === activeIndex % Contents.image.length,'transition-all ease-in-out duration-500 opacity-0 z-0 lg:opacity-100': index !== activeIndex % Contents.image.length}">
                <img :src="content.url" alt="images" loading="lazy" class="absolute top-0 lg:relative border-1 w-[420px] h-[480px] md:w-[720px] md:h-[580px] lg:w-[380px] lg:h-[580px]  object-cover">
            </div>
        </div>
    </main>
    <main class="flex justify-center align-center mt-[500px] md:mt-[600px] lg:mt-18">
        <h2 class="GeistMono text-left md:text-center text-black text-[14px] w-[738px] px-8 md:px-0" v-html="marked(Contents.description)"></h2>
    </main>
</template>