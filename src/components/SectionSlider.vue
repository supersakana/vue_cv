<template>
    <div class="text-xs text-[#566f91] flex gap-x-2 hover:text=[#556f90]">
        <div class="flex items-center hover:underline hover:text-[#4f79b0] cursor-pointer">
            <ion-icon name="arrow-up"></ion-icon>
            <span>Move Up</span>
        </div>

        <div class="flex items-center hover:underline hover:text-[#4f79b0] cursor-pointer">
            <ion-icon name="arrow-down"></ion-icon>
            <span>Move Down</span>
        </div>
    </div>
</template>
  
  <script>
  export default {
    name: 'SectionSlider'
  }
  </script>