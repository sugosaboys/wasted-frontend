<script setup>
import { onMounted } from 'vue'

onMounted(async () => {
  const AOS = await import('aos')
  await import('aos/dist/aos.css')
  AOS.init()
});
</script>

<template>
    <NuxtLayout>
        <NuxtPage/>
    </NuxtLayout>
</template>