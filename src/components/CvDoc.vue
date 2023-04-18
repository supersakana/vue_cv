<template>
  <div class="font-bold">
      <p>{{ contents.name }}</p>
      <p>{{ contents.email }}</p>
      <p>{{ contents.phone }}</p>

      <br>

      <p>{{ contents.university }}</p>
      <p>{{ contents.degree }}</p>
      <p>{{ contents.from_uni }}</p>
      <p>{{ contents.to_uni }}</p>

      <br>

      <p>{{ contents.company }}</p>
      <p>{{ contents.position }}</p>
      <p>{{ contents.description }}</p>
      <p>{{ contents.from_comp }}</p>
      <p>{{ contents.to_comp }}</p>
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