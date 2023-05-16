<template>
    <div id="skills-form" v-if="toggles['skills']">
      <div class="sub-form dark:border-[#364150]">
        <div  v-if="contents.skills.length !== 0 " class="form-control">
          <div :key="index" v-for="(skill, index) in contents.skills">
            <div :id="`skill-${index}`" class="flex items-center justify-center my-2">
                <input id='skills' 
                       type='text' 
                       :value="skill"
                       :data-id="index" 
                       placeholder="Enter a skill here..." 
                       @input="onInput($event, 'skills')"
                       class="w-full dark:bg-[#171e25] dark:text-white"
                  />
                <ion-icon class="text-gray-300 text-xl cursor-pointer ml-[14px] min-w-[16px] min-h-[16px]" @click="onDeleteSkill(index)" name="close-circle"></ion-icon>
            </div>
          </div>
        </div>
        <button class="button-bg my-3 px-4 py-2 font-bold text-white rounded-lg duration-500" @click="onAddSkill">Add Skill</button>
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