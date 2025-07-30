<template>
 <footer class="bg-[rgba(18,17,17,1)] pt-3 pb-5 px-6 md:px-40 text-sm">
  <main class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-x-8">
    <div class="mt-10">
        <img src="/public/icon/Logo.svg" alt="Wasted" loading="lazy" class="w-[105px]">
    </div>
    <div class="font-serif">
      <p class="ExposureTrialVARLight text-[#cec7be] mt-10 md:mt-10">About</p>
      <h2 class="ExposureTrialVAR text-white text-[16px] font-bold pt-[20px]">Wasted by Potato Head</h2>
      <p class="GeistMono text-[#ece6da] pt-[5px] text-[11px] tracking-[1px]">Wasted by Potato Head Transforms discarded materials into purposeful design, redefining waste as a material of the future.</p>
    </div>
     <div class="font-serif">
      <p class="ExposureTrialVARLight text-[#cec7be] mt-10 md:mt-10">Address</p>
      <h2 class="ExposureTrialVAR text-white text-[16px] font-bold pt-[20px]">Desa Potato Head</h2>
      <p class="GeistMono text-[#ece6da] pt-[5px] text-[11px] tracking-[1.2px]">Jalan Petitenget no. 51B, Seminyak, Kuta Utara, Kabupaten Badung, Bali — 80361, Indonesia</p>
    </div>
    <div class=" flex-col font-serif">
      <p class="ExposureTrialVARLight text-[#cec7be] mt-10 md:mt-10">Contacts</p>
      <div class="flex flex-col">
        <nuxt-link to="https://shop.potatohead.co/pages/faq#contact"><h2 class="ExposureTrialVAR hoverNavWhite flex text-white text-[16px] font-bold pt-[24px] gap-2 max-w-[110px] cursor-pointer"><img src="/icon/Vector.svg" alt="icon"  loading="lazy">Contact Us</h2></nuxt-link>
        <nuxt-link to="https://shop.potatohead.co/"> <h2 class="ExposureTrialVAR hoverNavWhite flex text-white text-[16px] font-bold pt-[6px] gap-2 max-w-[133px] cursor-pointer"><img src="/icon/Icon.svg" alt="icon" loading="lazy">Get Direction</h2></nuxt-link>
      </div>
    </div>
  </main>
  <main class="block md:flex justify-between items-center mt-18">
    <h2 class="GeistMonoThin text-[#cec7be] text-[12px] font-semibold">© 2023 Potato Head. PT Tiga Rasa. All Rights Reserved.</h2>
    <div class="GeistMono flex mt-5 md:mt-0 gap-6 pr-10">
      <nuxt-link to="https://shop.potatohead.co/pages/faq"><p class="GeistMonoThin text-white hoverNavWhite cursor-pointer text-[12px]">Privacy Policy</p></nuxt-link>
      <nuxt-link to=""><p class="GeistMonoThin text-white hoverNavWhite cursor-pointer text-[12px]">Terms & Conditions</p></nuxt-link>
    </div>
  </main>
</footer>

</template>
