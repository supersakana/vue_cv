<template>
  <div class="border p-3 m-3 w-[8in] h-[11in] bg-white p-[24px] font-roboto">
      <div class="text-center break-words flex flex-col gap-y-2">
        <p class="text-[30px]">{{ contents.name }}</p>
        <p class="px-[54px]">{{ contents.bio }}</p>
        <div class="flex justify-center gap-x-4">
          <p>{{ contents.location }}</p>
          <p>{{ contents.email }}</p>
          <p>{{ contents.phone }}</p>
        </div>
        <hr class="my-2 border-[#202020]">
      </div>

      <div class="flex flex-col gap-y-4">
        <div class="flex">
          <span class="font-bold basis-1/4">SKILLS</span>
          <p class=" basis-3/4">{{ contents.skills.join(', ') }}</p>
        </div>

        <div class="flex">
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

        <div class="flex">
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