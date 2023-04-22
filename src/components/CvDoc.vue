<template>
  <div class="font-bold">
      <p>{{ contents.name }}</p>
      <p>{{ contents.email }}</p>
      <p>{{ contents.phone }}</p>

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