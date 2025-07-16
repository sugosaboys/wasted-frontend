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
  <section class="grid grid-cols-1 md:grid-cols-2">
    <main v-for="content in Contents.slice(0,2)" class="flex justify-center align-center">
         <ContentCard :content="content" :URLIMAGES="URLIMAGES" />
    </main>
  </section>

  <section class="pt-10">
        <main v-for="content in Contents.slice(2,3)" class="flex justify-center align-center">
            <ContentCard :content="content" :URLIMAGES="URLIMAGES" />
        </main>
  </section>

   <section class="grid rid-cols-1 md:grid-cols-2 pt-10">
    <main v-for="content in Contents.slice(3,5)" class="flex justify-center align-center">
        <ContentCard :content="content" :URLIMAGES="URLIMAGES" />
    </main>
  </section>

   <section class="py-15">
        <main v-for="content in Contents.slice(5,6)" class="flex justify-center align-center">
           <ContentCard :content="content" :URLIMAGES="URLIMAGES" />
        </main>
  </section>
</template>
