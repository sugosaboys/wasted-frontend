<script setup>
   import { marked } from 'marked';
   const URLIMAGES = useRuntimeConfig().public.ApiURL;
   const { data: Contents, error } = await useFetch(
  `${URLIMAGES}/api/Followthe-waste`,
  {
    query:{
      'populate[hero]': 'true',
      'populate[HeroDescription]': 'true',
      'populate[CTA]': 'true',
      'populate[ImageWithCaption][populate]': ['image','ImageSecond','ImageThird' ,'ImageFourth'],
      'populate[ImageCaption][populate]': '*',
    },
    transform: res => res.data
  }
);
useHead({
        title:'Potato Head Wasted About',
        link : [
            {
                rel:'icon',
                href:'/icon/WastedLogo.png'
            }
        ]
});
</script>

<template>
   <max-width-container>
   <navbar/>
   <div class="pt-25">
      <h2 class=" text-left md:text-center text-[32px] md:text-[48px] ExposureTrialVARBold font-bold px-8 md:px-0 pt-5">{{ Contents.Title }}</h2>

      <section class="flex justify-center items-center pt-[45px] px-8 md:px-15 lg:px-0">
         <img :src="URLIMAGES + Contents.hero.url" alt="hero image" class="border-1 w-[380px] h-[380px] md:w-[800px] md:h-[400px] lg:w-[1200px] lg:h-[600px] object-cover" loading="lazy">
      </section>

      <main class="pt-[45px]">
         <section v-for="(text,index) in Contents.HeroDescription" :key="index" class="flex justify-center items-center pt-[15px]">
            <h2 class="GeistMono w-[732px] text-[14px] leading-tight text-justify px-8 md:px-0"  v-html="marked(text.TextDescription)"></h2>
         </section>
      </main>

      <section class="pt-[130px]">
            <main class="flex flex-col md:flex-row justify-center align-center gap-18">
               <div class="flex flex-col items-center">
                  <img :src="URLIMAGES + Contents.ImageWithCaption.image.url" alt="Images" loading="lazy" class="w-[312px] h-[312px] md:w-[400px] md:h-[400px] lg:w-[640px] lg:h-[640px] object-cover">
                  <p class="GeistMono w-[312px] md:400px lg:w-[640px] text-center text-[14px] font-bold">{{ Contents.ImageWithCaption.caption }}</p>
               </div>
               <div class="flex flex-col items-center">
                  <img :src="URLIMAGES + Contents.ImageWithCaption.ImageSecond.url" alt="Images" loading="lazy" class=" w-[312px] md:w-[300px] lg:w-[320px] h-[480px] object-cover">
                  <p class="GeistMono w-[312px] md:w-[320px] text-center text-[14px] font-bold">{{ Contents.ImageWithCaption.captionSecond }}</p>
               </div>
            </main>
            <main class="flex flex-col md:flex-row justify-center align-center gap-18 mt-20">
               <div class="flex flex-col items-center">
                  <img v-if="Contents.ImageWithCaption?.ImageThird?.url" :src="URLIMAGES + Contents.ImageWithCaption.ImageThird.url" alt="Images" loading="lazy" class="w-[540px] h-[810px] object-cover">
                  <p class="GeistMono w-[580px] text-center text-[14px] font-bold">{{ Contents.ImageWithCaption.captionThird }}</p>
               </div>
               <div class="flex flex-col items-center">
                  <img v-if="Contents.ImageWithCaption?.ImageFourth?.url" :src="URLIMAGES + Contents.ImageWithCaption.ImageFourth.url" alt="Images" loading="lazy" class="w-[480px] h-[480px] object-cover">
                  <p class="GeistMono w-[320px] text-center text-[14px] font-bold">{{ Contents.ImageWithCaption.captionFourth }}</p>
               </div>
            </main>
            <main class="flex justify-center align-center mt-0 md:mt-20">
               <h2 class="GeistMono w-[732px] text-[14px] leading-tight text-justify px-8 md:px-0" v-html="marked(Contents.ImageWithCaption.description)"></h2>
            </main>
      </section>

      <section class="pt-[130px]">
            <main class="flex flex-col md:flex-row justify-center align-center gap-18">
               <div class="flex flex-col items-center">
                  <img :src="URLIMAGES + Contents.ImageCaption.image.url" alt="Images" loading="lazy" class="w-[312px] h-[208px] md:w-[438px] md:h-[380px] lg:w-[720px] lg:h-[480px] object-cover">
                  <p class="GeistMono w-[320px] md:w-[438px] lg:w-[730px] text-center text-[14px] font-bold">{{ Contents.ImageCaption.caption }}</p>
               </div>
               <div class="flex flex-col items-center">
                  <img :src="URLIMAGES + Contents.ImageCaption.ImageSecond.url" alt="Images" loading="lazy" class="w-[320px] h-[320px] object-cover">
                  <p class="GeistMono w-[320px] text-center text-[14px] font-bold">{{ Contents.ImageCaption.captionSecond }}</p>
               </div>
            </main>
            <main class="flex flex-col md:flex-row justify-center align-center gap-18 mt-20">
               <div class="flex flex-col items-center">
                  <img :src="URLIMAGES + Contents.ImageCaption.ImageThird.url" alt="Images" loading="lazy" class="w-[312px] h-[468px] md:w-[400px] md:h-[610px] lg:w-[540px] lg:h-[810px] object-cover">
                  <p class="GeistMono w-[320px] md:w-[400px] lg:w-[580px] text-center text-[14px] font-bold">{{ Contents.ImageCaption.captionThird }}</p>
               </div>
               <div class="flex flex-col items-center">
                  <img :src="URLIMAGES + Contents.ImageCaption.ImageFourth.url" alt="Images" loading="lazy" class="w-[312px] md:w-[380px] lg:w-[480px] h-[480px] object-cover">
                  <p class="GeistMono w-[312px] md:w-[400px] lg:w-[500px] text-center text-[14px] font-bold">{{ Contents.ImageCaption.captionSecond }}</p>
               </div>
            </main>
             <main class="flex justify-center align-center mt-20">
               <h2 class="GeistMono w-[732px] text-[14px] leading-tight text-justify px-8 md:px-0" v-html="marked(Contents.ImageCaption.description)"></h2>
            </main>
      </section>

      <FollowtheWastePageCTAbutton class="flex justify-center align-center mt-[55px] mb-[55px] font-bold">
         <li class="flex align-center hoverNav hover:text-[#0d7dbb] cursor-pointer group">
               <NuxtLink :to="Contents.CTA.URL" class="ExposureTrialVAR">{{ Contents.CTA.Title }}</NuxtLink>
               <img src="/icon/Arrowup-right.svg" alt="-" class="w-[12px] h-[12px] mt-2 ml-1 block group-hover:hidden" loading="lazy">
               <img src="/icon/Arrowup-right-blue.svg" alt="-" class="w-[12px] h-[12px] mt-2 ml-1 hidden group-hover:block" loading="lazy">
         </li>
      </FollowtheWastePageCTAbutton>
   </div>
   <Footer/>
   </max-width-container>
</template>