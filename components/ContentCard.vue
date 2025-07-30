<template>
    <NuxtLink v-if="content.content" :to="`/${content.content.Slug}`">
    <div class="flex flex-col cursor-pointer group">
            <img :src="URLIMAGES + content.image[0].url" alt="images" class="absolute w-[320px] h-[320px] md:w-[350px] md:h-[350px] md:h-[350px] lg:w-[430px] lg:h-[430px] object-cover transition-opacity duration-500 ease-in-out opacity-100 group-hover:opacity-0 mt-16 mb-4" loading="lazy" />
            <img :src="URLIMAGES + content.hover.url" alt="images" class="w-[320px] h-[320px] md:w-[350px] md:h-[350px] lg:w-[430px] lg:h-[430px] object-cover transition-opacity duration-500 ease-in-out opacity-0  group-hover:opacity-100 group-hover:border-1 mt-16 mb-4" loading="lazy">
            <h2 class="transition-all duration-500 ease-in-out text-[21px] font-serif font-bold  py-1 ExposureTrialVAR  group-hover:text-[#0d7dbb] group-hover:border-black">{{ content.Title }}</h2>
            <div class="transition-all duration-500 ease-in-out flex justify-between align-center border-[#a6a6a6] border-t-1 border-b-1 py-1 mt-2 font-serif group-hover:border-black">
                <p class="transition-all duration-500 ease-in-out GeistMono text-[#4e4746] text-[13px] group-hover:text-black">Material:</p>
                <p class="transition-all duration-500 ease-in-out GeistMono text-[#4e4746] text-[13px] font-bold group-hover:text-black">{{ content.Material }}</p>
            </div>
             <div class="transition-all duration-500 ease-in-out flex justify-between align-center border-[#a6a6a6] border-b-1 py-1 font-serif group-hover:border-black">
                <p class="transition-all duration-500 ease-in-out GeistMono text-[#4e4746] text-[13px] group-hover:text-black">Process:</p>
                <p class="transition-all duration-500 ease-in-out GeistMono text-[#4e4746] text-[13px] font-bold group-hover:text-black">{{ content.Process }}</p>
            </div>
             <div class="transition-all duration-500 ease-in-out flex justify-between align-center border-[#a6a6a6] border-b-1 group-hover: py-1 font-serif group-hover:border-black">
                <p class="transition-all duration-500 ease-in-out GeistMono text-[#4e4746] text-[13px] group-hover:text-black">Function:</p>
                <p class="transition-all duration-500 ease-in-out GeistMono text-[#4e4746] text-[13px] font-bold group-hover:text-black">{{ content.Function }}</p>
            </div>
        </div>
        </NuxtLink>
</template>

<script setup>
    defineProps({
        content:Object,
        URLIMAGES:String
    });
</script>