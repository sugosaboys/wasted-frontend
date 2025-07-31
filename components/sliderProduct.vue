<script setup>
    const URLIMAGES = useRuntimeConfig().public.ApiURL;

    const { data: sliderImages, error } = await useFetch(`${URLIMAGES}/api/slider-content`, {
    query: {
        populate: '*'
    },
    transform: (res) => res.data.image
    });
</script>

<template>
    <main data-aos="fade-zoom-in" data-aos-duration="1000" class="flex justify-center align-center">
        <div class="slider py-20">
            <div class="item flex">
                <img v-for="(item, index) in sliderImages" :key="index" :src=" item.url" :alt="item.name" loading="lazy" />
                <img v-for="(item, index) in sliderImages" :key="index" :src=" item.url" :alt="item.name" loading="lazy" />
                <img v-for="(item, index) in sliderImages" :key="index" :src=" item.url" :alt="item.name" loading="lazy" />
            </div>
        </div>
    </main>
</template>