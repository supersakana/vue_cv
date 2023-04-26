<template>
    <div id="skills-form" v-if="toggles['skills']">
      <div id="add-skill" class="flex items-center">
        <input id='skills' 
               type='text' 
               placeholder="Enter a skill here..." 
        />
        <ion-icon name="add-circle" class="text-green-600 text-xl cursor-pointer" @click="onAddSkill"></ion-icon>
      </div>

    </div>
  </template>
  
  <script>
  export default {
    name: 'SkillsForm',
    props: {
      contents: Object,
      toggles: Object
      },
    methods: {
        onAddSkill(){
          const form = document.querySelector('#skills')
          this.$emit('add-skill', form.value)
          form.value = ''
        }
        // onDeleteSkill
    },
  }
  </script>