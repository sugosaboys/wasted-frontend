<script setup>
const URLIMAGES = useRuntimeConfig().public.ApiURL;

const { data: Contents, error} = await useFetch(`${URLIMAGES}/api/products-glimpses`,{
    query: {
        sort:'order',
        populate: '*'
    },
    transform: (res) => res.data
});
</script>


<template>
  <section class="grid grid-cols-1 md:grid-cols-2 gap-4 pb-10">
    <main data-aos="fade-up" data-aos-duration="1000" v-for="(content,index) in Contents" :key="index" :class="['flex justify-center align-center',(index + 1) % 3 === 0 ? 'md:col-span-2 justify-center' : '']">
         <ContentCard :content="content" :URLIMAGES="URLIMAGES" />
    </main>
  </section>
</template>
