<template>
    <div id="skills-form" v-if="toggles['skills']">
      <div class="sub-form">
        <div class="form-control">
          <div :key="index" v-for="(skill, index) in contents.skills">
            <div :id="`skill-${index}`" class="flex items-center my-2">
                <input id='skills' 
                  type='text' 
                  :value="skill"
                  :data-id="index" 
                  placeholder="Enter a skill here..." 
                  @input="onInput($event, 'skills')"
                  />
                <ion-icon name="remove-circle" class="text-red-600 text-xl cursor-pointer" @click="onDeleteSkill(index)"></ion-icon>
            </div>
          </div>
        </div>
        <button class="button-bg mb-3 mt-1 px-4 py-2 font-bold text-white rounded-lg duration-500" @click="onAddSkill">Add Skill</button>
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
          this.$emit('add-skill', 'Add a skill')
        },
        onDeleteSkill(index){
          this.$emit('delete-skill', index)
        },
        onInput(e, form){
          this.$emit('update-contents', e, form)
        },
    },
  }
  </script>