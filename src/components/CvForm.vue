<template>
  <form @submit.prevent="onSubmit" class="h-screen overflow-y-scroll shadow-md py-1 px-3">

      <!-- General -->
    <div>
      <div class="flex items-center">
        <ion-icon name="chevron-down-outline" @click="onFormToggle($event, 'general')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
        <h4 className="section-title">General</h4>
      </div>
      <GeneralForm :contents="contents" :toggles="toggles" @update-contents="updateContents" />
    </div>

    <!-- Skills -->
    <div>
      <div class="flex items-center">
        <ion-icon name="chevron-down-outline" @click="onFormToggle($event, 'skills')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
        <h4 className="section-title">Skills</h4>
      </div>
      <SkillsForm :contents="contents" :toggles="toggles"  @add-skill="addSkill"  @delete-skill="deleteSkill" />
    </div>

      <!-- Education -->

    <div>
      <div class="flex items-center">
        <ion-icon name="chevron-down-outline" class="cursor-pointer hover:text-gray-600 text-2xl" @click="onFormToggle($event, 'education')"></ion-icon>
        <h4 className="section-title">Education</h4>
      </div>
      <EducationForm :contents="contents" 
                      :toggles="toggles" 
                      @update-contents="updateContents"  
                      @delete-form="deleteForm" 
                      @add-form="addForm" />
    </div>

      <!-- Experience -->

    <div>
      <div class="flex items-center">
        <ion-icon name="chevron-down-outline" @click="onFormToggle($event, 'experience')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
        <h4 className="section-title">Experience</h4>
      </div>
      <ExperienceForm :contents="contents" 
                      :toggles="toggles" 
                      @update-contents="updateContents"  
                      @delete-form="deleteForm" 
                      @add-form="addForm" />
    </div>

    <input type='submit' value='Submit' className="bg-blue-500 text-white rounded-md py-1 px-2 hover:bg-blue-400 duration-500" />
  </form>
</template>

<script>
import GeneralForm from './forms/GeneralForm.vue'
import EducationForm from './forms/EducationForm.vue'
import ExperienceForm from './forms/ExperienceForm.vue'
import SkillsForm from './forms/SkillsForm.vue'

export default {
  name: 'CvForm',
  components: {
    GeneralForm,
    SkillsForm,
    EducationForm,
    ExperienceForm,
  },
  props: {
    contents: Object
    },
  methods: {
    onSubmit(e) {
      e.preventDefault
      this.$emit('export-pdf')
    },
    updateContents(e, form){
      this.$emit('update-contents', e, form)
    },
    onFormToggle(e, form){
      const updated = this.toggles
      updated[form] = !updated[form]
      this.toggles = updated

      e.target.name === 'chevron-up-outline' ? 
      e.target.name = 'chevron-down-outline' : e.target.name = 'chevron-up-outline'
    },
    addForm(form){
      this.$emit('add-form', form)
    },
    deleteForm(form, id){
      this.$emit('delete-form', form, id)
    },
    addSkill(skill){
      this.$emit('add-skill', skill)
    },
    deleteSkill(index){
      this.$emit('delete-skill', index)
    }
  },
  data(){
    return {
      toggles: {
        general: true,
        skills: true,
        education: true,
        experience: true,
      }
    }
  },
}
</script>

<style>
.form-control {
  display: flex;
  gap: 5px;
  margin-top: 2px;
}

.section-title {
  font-weight: bold;
  font-size: 1.5rem;
}
</style>