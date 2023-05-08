<template>
  <div class="shadow-lg p-3 m-3 w-[8in] h-[11in] bg-white p-[24px] font-roboto">
    <!-- General -->
      <div class="text-center break-words flex flex-col gap-y-2">
        <p class="text-[30px]">{{ contents.name }}</p>
        <p class="px-[54px]">{{ contents.bio }}</p>
        <div class="flex justify-center gap-x-4">
          <p>{{ contents.location }}</p>
          <p>{{ contents.email }}</p>
          <p>{{ contents.phone }}</p>
        </div>

        <!-- Socials -->
        <div class="flex justify-center gap-x-3 flex-wrap">
          <div v-if="contents.linkedin !== ''" class="flex items-center justify-center gap-x-1">
            <ion-icon name="logo-linkedin"></ion-icon>
            <a class="text-[12px] hover:underline" :href="contents.linkedin">{{ contents.linkedin }}</a>
          </div>

          <div v-if="contents.twitter !== ''" class="flex items-center justify-center gap-x-1">
            <ion-icon name="logo-twitter"></ion-icon>
            <a class="text-[12px] hover:underline" :href="contents.twitter">{{ contents.twitter }}</a>
          </div>

          <div v-if="contents.github !== ''" class="flex items-center justify-center gap-x-1">
            <ion-icon name="logo-github"></ion-icon>
            <a class="text-[12px] hover:underline" :href="contents.github">{{ contents.github }}</a>
          </div>

          <div v-if="contents.instagram !== ''" class="flex items-center justify-center gap-x-1">
            <ion-icon name="logo-instagram"></ion-icon>
            <a class="text-[12px] hover:underline" :href="contents.instagram">{{ contents.instagram }}</a>
          </div>

          <div v-if="contents.facebook !== ''" class="flex items-center justify-center gap-x-1">
            <ion-icon name="logo-facebook"></ion-icon>
            <a class="text-[12px] hover:underline" :href="contents.facebook">{{ contents.facebook }}</a>
          </div>
        </div>
        <hr class="my-2 border-[#202020]">
      </div>

      <!-- Skills -->
      <div class="flex flex-col gap-y-4">
        <div v-if="contents.skills.length !== 0 " class="flex">
          <span class="font-bold basis-1/4">SKILLS</span>
          <p class=" basis-3/4">{{ contents.skills.join(', ') }}</p>
        </div>

        <!-- Education -->
        <div v-if="contents.education.length !== 0 " class="flex">
          <span class="font-bold basis-1/4">EDUCATION</span>
          <div class="basis-3/4 flex flex-col gap-y-1">
            <div :key="edu.id" v-for="edu in contents.education">
              <div class="flex justify-between">
                <p class="font-bold">{{ edu.university }}</p>
                <p>{{ `${edu.from_uni} - ${edu.to_uni}` }}</p>
              </div>
              <p>{{ edu.degree }}</p>
            </div>
          </div>
        </div>

        <!-- Experience -->
        <div  v-if="contents.experience.length !== 0 " class="flex">
          <span class="font-bold basis-1/4">EXPERIENCE</span>
          <div class="basis-3/4 flex flex-col gap-y-1">
            <div :key="exp.id" v-for="exp in contents.experience">
              <div class="flex justify-between">
                <p class="font-bold">{{ exp.company }}</p>
                <p>{{ `${exp.from_comp} - ${exp.to_comp}` }}</p>

              </div>
              <p>{{ exp.position }}</p>
              <p class="whitespace-pre">{{ exp.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
  export default {
  name: 'CvDoc',
  props: {
    contents: Object
    },
}
</script>