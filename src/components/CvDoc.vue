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
        <hr class="my-1 border-[#202020]">
      </div>

      <br>

      <p>{{ contents.skills.join(', ') }}</p>

      <br>

      <div :key="edu.id" v-for="edu in contents.education">
        <p>{{ edu.university }}</p>
        <p>{{ edu.degree }}</p>
        <p>{{ edu.from_uni }}</p>
        <p>{{ edu.to_uni }}</p>
      </div>

      <br>

      <div :key="exp.id" v-for="exp in contents.experience">
        <p>{{ exp.company }}</p>
        <p>{{ exp.position }}</p>
        <p class="whitespace-pre">{{ exp.description }}</p>
        <p>{{ exp.from_comp }}</p>
        <p>{{ exp.to_comp }}</p>
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