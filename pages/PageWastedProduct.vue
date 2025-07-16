<script setup>

const URLIMAGES = useRuntimeConfig().public.ApiURL;
const { data: content, error } = await useFetch(`${URLIMAGES}/api/products`, {
  query: {
    populate:'*'
  },
  transform: (res) => res.data
}); 

console.log('Response dari API:', content.value);
const sliceCount = ref(16);
const increment = 4;

const loadMore  = ()=>{
    if(content.value && sliceCount.value < content.value.length){
        sliceCount.value += increment;
    }
};
</script>

<template>
    <max-width-container>
    <navbar/>
    <h2 class="text-[32px] md:text-[48px] ExposureTrialVARBold font-bold md:text-center pt-[120px] px-8 md:px-0">wasted products</h2>
    <section class="flex justify-center align-center pt-10 pb-10">
        <main class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
            <div v-for="(product , index) in content.slice(0,sliceCount)" :key="index">
                <img :src="product.image.url" alt="products" loading="lazy" class="w-[318px] h-[312px] md:w-[256px] md:h-[256px]">
                <h3 class="text-center ExposureTrialVAR font-bold text-[16px] mt-5">{{ product.textShort }}</h3>
                <div class="flex justify-center align-center">
                    <nuxt-link :to="product.CTA.URL" class="flex mt-2 hoverNav group">
                        <p class="ExposureTrialVAR font-bold text-[14px] group-hover:text-[#0d7dbb]">{{ product.CTA.Title }}</p>
                        <img src="/icon/Arrowup-right.svg"  alt="Arrowup-right" class="ml-1 block group-hover:hidden" loading="lazy">
                        <img src="/icon/Arrowup-right-blue.svg"  alt="Arrowup-right" class="ml-1 hidden group-hover:block" loading="lazy">
                    </nuxt-link>
                </div>
            </div>
        </main>
    </section>

    <div class="flex justify-center align-center pt-10 pb-16">
        <h2 class="GeistMono hoverNav text-center hover:text-[#0d7dbb] cursor-pointer" @click="loadMore">Load More</h2>
    </div>
    <Footer/>
    </max-width-container>
</template>