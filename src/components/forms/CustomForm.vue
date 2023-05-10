<template>
    <div :id="section.title.toLowerCase() + '-' + index" v-if="section.toggle">
        <p>Sub form will go here</p>
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
    //   onInput(e, section){
    //     update form content etc...
    //   },
      onAddForm(form){
        this.$emit('add-form', form)
      },
      onDeleteForm(form, id){
        this.$emit('delete-form', form, id)
      }
    },
  }
  </script>