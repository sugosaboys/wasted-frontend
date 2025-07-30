<script setup>
import { marked } from 'marked';
import { useRoute } from 'vue-router';
import { ref } from 'vue';

const URLIMAGES = useRuntimeConfig().public.ApiURL;
const route = useRoute();
const slug = route.params.slug;

const { data: content, error } = await useFetch(`${URLIMAGES}/api/contents`, {
  query: {
    'filters[Slug][$eq]': slug,
    'populate[BackButton]': 'true',
    'populate[composition]': 'true',
    'populate[CTA]': 'true',
    'populate[products][populate]': ['image' , 'CTA'],
    'populate[ImageWithCaption][populate]': ['image','ImageSecond','ImageThird' ,'ImageFourth'],
    'populate[ImageCaption][populate]': '*'
  },
  transform: (res) => res.data[0]
}); 


const itemWidth = 325;
const visibleWidth = ref(0);
const Left = ref(0);
const opacityRightRow = ref(1);
const opacityLeftRow = ref(0.2);

onMounted(() => {
  const sliderEl = document.querySelector('.slider-container');
  visibleWidth.value = sliderEl?.offsetWidth || 1200;
});

const maxScroll = computed(() => {
  if (!content.value?.products) return 0;
  const totalWidth = content.value.products.length * itemWidth;
  return -(totalWidth - visibleWidth.value);
});

const Decrease = () => {
  if (Left.value > maxScroll.value) {
    Left.value -= itemWidth;
    if (Left.value <= maxScroll.value) {
      Left.value = maxScroll.value;
      opacityRightRow.value = 0.2;
    } else {
      opacityRightRow.value = 1;
    }
    opacityLeftRow.value = 1;
  }
};

const Increase = () => {
  if (Left.value < 0) {
    Left.value += itemWidth;
    if (Left.value >= 0) {
      Left.value = 0;
      opacityLeftRow.value = 0.2;
    } else {
      opacityLeftRow.value = 1;
    }
    opacityRightRow.value = 1;
  }
};

</script>

<template>
  <navbar/>
  <section class="flex md:justify-center items-center pt-[120px] px-8 md:px-0">
    <div>
      <ul class="flex md:justify-center align-center">
        <nuxt-link :to="content.BackButton.URL">
        <li class="flex justify-center align-center text-center text-[#1b181a] list-none font-bold group hoverNav gap-2">
            <img src="/icon/ArrowLeft.svg" alt="ArrowLeft" class="mt-[1px] block group-hover:hidden animate" loading="lazy"> 
            <img src="/icon/ArrowLeftBlue.svg" alt="ArrowLeftBlue" class="mt-[1px] hidden group-hover:block animate" loading="lazy"> 
            <p class="ExposureTrialVAR group-hover:text-[#0d7dbb] cursor-pointer">{{ content.BackButton.Title }}</p>
        </li>
        </nuxt-link>
      </ul>
      <h1 class="ExposureTrialVARBold text-[#1b181a] text-[32px] md:text-[48px] text-center font-bold">{{ content.Title }}</h1>
    </div>
  </section>

  <section class="flex md:justify-center align-center mt-10 px-8 md:px-0">
    <div class="w-[205px] md:w-[806px]">
        <p class="GeistMono text-left text-[14px]" v-html="content.DesignerField"></p>
    </div>
  </section>

  <section class="flex md:justify-center align-center mt-5 px-8 md:px-0">
    <main>
      <div v-for="Contens in content.composition" class="GeistMono flex flex-col md:flex-row md:justify-between md:w-[806px] text-[#1b181a]">
            <p>{{ Contens.Title }}</p>
            <p class="md:text-right">{{ Contens.subTitle }}</p>
      </div>
    </main>
  </section>

  <section class="flex md:justify-center align-center mt-2 px-8 md:px-0">
    <main>
      <div v-for="Contens in content.composition" class="GeistMono flex flex-col md:flex-row md:justify-between text-[#1b181a] border-[#b6aea8] border-b-1  md:w-[806px] text-[14px] py-2">
            <p>{{ Contens.Composition }}</p>
            <p class="md:text-right">{{ Contens.details }}</p>
      </div>
    </main>
  </section>

  <section class="pt-[130px]">
    <main class="flex flex-col md:flex-row justify-center align-center gap-18">
        <div class="flex flex-col items-center">
            <img v-if="content.ImageWithCaption?.image?.url" :src=" content.ImageWithCaption.image.url" alt="Images" loading="lazy" class="border-1 w-[320px] h-[320px] object-cover">
            <p v-if="content.ImageWithCaption?.caption" class="w-[320px] GeistMono font-bold text-[14px] text-center">{{ content.ImageWithCaption.caption }}</p>
        </div>
        <div class="flex flex-col items-center">
            <img v-if="content.ImageWithCaption?.ImageSecond?.url" :src=" content.ImageWithCaption.ImageSecond.url" alt="Images" loading="lazy" class="border-1 w-[318px] h-[210px] md:w-[420px] md:h-[400px] lg:w-[720px] lg:h-[480px] object-cover">
            <p v-if="content.ImageWithCaption?.captionSecond" class="w-[312px] md:w-[418px] lg:w-[730px] GeistMono font-bold text-[14px] text-center">{{ content.ImageWithCaption.captionSecond }}</p>
        </div>
    </main>
    <main class="flex flex-col md:flex-row justify-center align-center gap-18 mt-20">
        <div class="flex flex-col items-center">
            <img v-if="content.ImageWithCaption?.ImageThird?.url" :src=" content.ImageWithCaption.ImageThird.url" alt="Images" loading="lazy" class="border-1 w-[318px] h-[312px] md:w-[420px] md:h-[400px] lg:w-[640px] lg:h-[640px] object-cover">
            <p v-if="content.ImageWithCaption?.captionThird" class="w-[312px] md:w-[418px] lg:w-[650px] GeistMono font-bold text-[14px] text-center">{{ content.ImageWithCaption.captionThird }}</p>
        </div>
        <div class="flex flex-col items-center">
            <img v-if="content.ImageWithCaption?.ImageFourth?.url" :src=" content.ImageWithCaption.ImageFourth.url" alt="Images" loading="lazy" class="border-1 w-[318px] md:w-[320px] h-[480px] object-cover">
            <p v-if="content.ImageWithCaption?.captionFourth" class="w-[320px] GeistMono font-bold text-[14px] text-center">{{ content.ImageWithCaption.captionFourth }}</p>
        </div>
    </main>
    <main class="flex justify-center align-center mt-20 px-8 md:px-0">
        <h2 v-if="content.ImageWithCaption?.description" class="GeistMono w-[732px] text-[15px] text-justify" v-html="marked(content.ImageWithCaption.description)"></h2>
    </main>
  </section>

   <section class="pt-[130px]">
    <main class="flex flex-col md:flex-row justify-center align-center gap-18">
        <div class="flex flex-col items-center">
            <img v-if="content.ImageCaption?.image?.url" :src=" content.ImageCaption.image.url" alt="Images" loading="lazy" class="border-1 w-[318px] h-[312px] md:w-[420px] md:h-[400px] lg:w-[640px] lg:h-[640px] object-cover">
            <p v-if="content.ImageCaption?.caption" class="w-[320px] md:w-[418px] lg:w-[680px] GeistMono font-bold text-[14px] text-center">{{ content.ImageCaption.caption }}</p>
        </div>
        <div class="flex flex-col items-center">
            <img v-if="content.ImageCaption?.ImageSecond?.url" :src=" content.ImageCaption.ImageSecond.url" alt="Images" loading="lazy" class="border-1 w-[312px] h-[312px] md:w-[320px] md:h-[320px] object-cover">
            <p v-if="content.ImageCaption?.captionSecond" class="w-[320px] GeistMono font-bold text-[14px] text-center">{{ content.ImageCaption.captionSecond }}</p>
        </div>
    </main>
    <main class="flex flex-col md:flex-row justify-center align-center gap-18 mt-20">
        <div class="flex flex-col items-center">
            <img v-if="content.ImageCaption?.ImageThird?.url" :src=" content.ImageCaption.ImageThird.url" alt="Images" loading="lazy" class="border-1 w-[318px] h-[468px] md:w-[360px] md:h-[540px] object-cover">
            <p v-if="content.ImageCaption?.captionThird" class="w-[320px] GeistMono font-bold text-[14px] text-center">{{ content.ImageCaption.captionThird }}</p>
        </div>
        <div class="flex flex-col items-center">
            <img v-if="content.ImageCaption?.ImageFourth?.url" :src=" content.ImageCaption.ImageFourth.url" alt="Images" loading="lazy" class="border-1 w-[318px] h-[468px] md:w-[320px] md:h-[640px] lg:w-[640px] lg:h-[940px] object-cover">
            <p v-if="content.ImageCaption?.captionFourth" class="w-[320px] md:w-[418px] lg:w-[680px] GeistMono font-bold text-[14px] text-center">{{ content.ImageCaption.captionFourth }}</p>
        </div>
    </main>
    <main class="flex justify-center align-center mt-20 px-8 md:px-0">
        <h2 v-if="content.ImageCaption?.description" class="GeistMono w-[732px] text-[14px] text-justify" v-html="marked(content.ImageCaption.description)"></h2>
    </main>
  </section>

  <section class="flex justify-center items-center pt-[55px]">
    <div>
      <nuxt-link :to="content.CTA.URL">
      <li class="flex text-center list-none font-bold hoverNav group">
        <p class="ExposureTrialVAR group-hover:text-[#0d7dbb] ">{{ content.CTA.Title }}</p>
        <img src="/icon/Arrowup-right.svg" alt="arrowUpRight" class="ml-[5px] mt-[1px] block group-hover:hidden" loading="lazy">
        <img src="/icon/Arrowup-right-blue.svg" alt="arrowUpRight" class="ml-[5px] mt-[1px] hidden group-hover:block" loading="lazy">
      </li>
      </nuxt-link>
    </div>
  </section>

  <section class="flex justify-center align-center mt-30 px-8 md:px-8 lg:px-0">
    <main class="flex justify-between align-center w-[1120px]">
      <h2 class="ExposureTrialVAR font-bold text-[22px]">{{ content.subTitle }}</h2>
      <div class="flex gap-8">
        <img src="/icon/ArrowLeft.svg" alt="LeftSlide" class="w-[28px] cursor-pointer" :style="{opacity : opacityLeftRow}" loading="lazy" @click="Increase">
        <img src="/icon/ArrowRight.svg" alt="RightSlide" class="w-[28px] cursor-pointer" :style="{opacity : opacityRightRow}" loading="lazy" @click="Decrease">
      </div>
    </main>
  </section>

<Slider class="slider-container scrollbarHidden overflow-x-auto overflow-y-auto pb-10 px-8 md:px-0">
    <section class="transition-all duration-600 ease-in-out flex gap-8 relative md:px-50" :style="{left: Left + 'px'}"> 
      <div v-for="(plasticProducts,index) in content.products" :key="index" class="pt-[45px]">       
        <div class="flex flex-col items-center w-[256px]">         
          <img :src=" plasticProducts.image.url" alt="Plastic Product Image" class="w-[256px] h-[256px] object-cover" loading="lazy">
          <h3 class="text-center ExposureTrialVAR font-bold text-[16px] mt-5">{{ plasticProducts.textShort }}</h3>        
          <nuxt-link :to="plasticProducts.CTA.URL" class="flex mt-2 hoverNav group">
            <p class="ExposureTrialVAR font-bold text-[14px] group-hover:text-[#0d7dbb]">{{ plasticProducts.CTA.Title }}</p>
            <img src="/icon/Arrowup-right.svg"  alt="Arrowup-right" class="ml-1 block group-hover:hidden" loading="lazy">
            <img src="/icon/Arrowup-right-blue.svg"  alt="Arrowup-right" class="ml-1 hidden group-hover:block" loading="lazy">
          </nuxt-link>    
        </div>    
      </div>
    </section>
</Slider>

<Footer/>
</template>

<style scoped>

.animate{
  animation: rotateX .4s 1 ease-in-out;
}

  @keyframes rotateX{
    from{
      transform: rotateY(0deg);
    }
    to{
      transform: rotateY(360deg);
    }
  }
</style>