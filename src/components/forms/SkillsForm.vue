<template>
    <div id="skills-form" v-if="toggles['skills']">
      <div class="sub-form">
          <div className="form-control">
            <div id="add-skill" class="flex items-center justify-between">
            <input id='skills' 
                  type='text' 
                  placeholder="Enter a skill here..." 
            />
            <ion-icon name="add-circle" class="text-green-600 text-xl cursor-pointer" @click="onAddSkill"></ion-icon>
          </div>
        </div>

        <div class="form-control">
          <div :key="index" v-for="(skill, index) in contents.skills">
            <div :id="`skill-${index}`" class="flex items-center justify-between">
                <!-- <span>{{ skill }}</span> -->
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
          if(form.value === '') return

          this.$emit('add-skill', form.value)
          form.value = ''
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