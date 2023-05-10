<template>
    <div id="projects-1" v-if="section.toggle">
        <span>{{ section }}</span>
        <span>{{ index }}</span>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CustomForm',
    props: {
      section: Object,
      index: Number
      },
    methods: {
      onInput(e, form){
        this.$emit('update-contents', e, form)
      },
      onAddForm(form){
        this.$emit('add-form', form)
      },
      onDeleteForm(form, id){
        this.$emit('delete-form', form, id)
      }
    },
  }
  </script>