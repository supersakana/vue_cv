<template>
  <form @submit.prevent="onSubmit" class="h-screen overflow-y-scroll shadow-md py-1 px-3 flex flex-col">

    <!-- General -->
    <div class="mx-4 my-2">
      <div class="flex items-center">
        <ion-icon name="chevron-down-outline" @click="onFormToggle($event, 'general')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
        <h4 className="section-title">General</h4>
      </div>
      <GeneralForm :contents="contents" :toggles="toggles" @update-contents="updateContents" />
    </div>

    <!-- Social -->
    <div class="mx-4 my-2">
      <div class="flex items-center">
        <ion-icon name="chevron-down-outline" @click="onFormToggle($event, 'social')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
        <h4 className="section-title">Social</h4>
      </div>
      <SocialForm :contents="contents" :toggles="toggles" @update-contents="updateContents" />
    </div>

    <!-- Skills -->
    <div class="mx-4 my-2">
      <div class="flex items-center">
        <ion-icon name="chevron-down-outline" @click="onFormToggle($event, 'skills')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
        <h4 className="section-title">Skills</h4>
      </div>
      <SkillsForm :contents="contents"
                  :toggles="toggles"  
                  @add-skill="addSkill"  
                  @delete-skill="deleteSkill"
                  @update-contents="updateContents" />
                  
    </div>

    <!-- Education -->

    <div class="mx-4 my-2">
      <div class="flex justify-between">
        <div class="flex items-center">
          <ion-icon name="chevron-down-outline" class="cursor-pointer hover:text-gray-600 text-2xl" @click="onFormToggle($event, 'education')"></ion-icon>
          <h4 className="section-title">Education</h4>
        </div>

        <SectionSlider />
      </div>

      <EducationForm :contents="contents" 
                     :toggles="toggles" 
                     @update-contents="updateContents"  
                     @delete-form="deleteForm" 
                     @add-form="addForm" />
    </div>

      <!-- Experience -->

    <div class="mx-4 my-2">
      <div class="flex justify-between">
        <div class="flex items-center">
          <ion-icon name="chevron-down-outline" @click="onFormToggle($event, 'experience')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
          <h4 className="section-title">Experience</h4>
        </div>

        <SectionSlider />
        
      </div>

      <ExperienceForm :contents="contents" 
                      :toggles="toggles" 
                      @update-contents="updateContents"  
                      @delete-form="deleteForm" 
                      @add-form="addForm" />
    </div>

    <!-- Custom -->
    <CustomSections :contents="contents" 
                    :toggles="toggles" 
                    @update-contents="updateContents"  
                    @delete-form="deleteForm" 
                    @add-form="addForm" />

    <button class="mt-auto button-bg my-6 mx-4 px-4 py-2 font-bold text-white rounded-lg duration-500"  @click="onAddSection">Add Custom Section</button>
  </form>
</template>

<script>
import GeneralForm from './forms/GeneralForm.vue'
import SocialForm from './forms/SocialForm.vue'
import SkillsForm from './forms/SkillsForm.vue'
import EducationForm from './forms/EducationForm.vue'
import ExperienceForm from './forms/ExperienceForm.vue'
import CustomSections from './CustomSections.vue'
import SectionSlider from './SectionSlider.vue'

export default {
  name: 'CvForm',
  components: {
    GeneralForm,
    SkillsForm,
    EducationForm,
    ExperienceForm,
    SocialForm,
    CustomSections,
    SectionSlider,
  },
  props: {
    contents: Object
    },
  methods: {
    onSubmit(e) {
      e.preventDefault
      // this.$emit('export-pdf')
    },
    updateContents(e, form){
      this.$emit('update-contents', e, form)
    },
    onFormToggle(e, form){
      const updated = this.toggles
      updated[form] = !updated[form]
      this.toggles = updated

      e.target.name === 'chevron-down-outline' ? 
      e.target.name = 'chevron-up-outline' : e.target.name = 'chevron-down-outline'
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
    },
    onAddSection(){
      this.$emit('add-section')
    }
  },
  data(){
    return {
      toggles: {
        general: true,
        social: true,
        skills: true,
        education: true,
        experience: true,
      }
    }
  },
  create(){
    if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
      document.documentElement.classList.add('dark')
    } else {
      document.documentElement.classList.remove('dark')
    }
  }
}
</script>

<style>

.form-control {
  display: flex;
  flex-direction: column;
  gap: 5px;
  margin: 15px 0;
}

.sub-form {
  border: solid #d1d9e4 1px;
  box-shadow: #cccccc1a 0px 1px 3px 0px, rgba(219, 219, 219, 0.06) 0px 1px 2px 0px;
  border-radius: 8px;
  padding: 4px 20px;
}

.section-title {
  font-weight: bold;
  font-size: 1.5rem;
  margin: 15px 0;
}
</style>