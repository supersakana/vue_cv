<template>
  <form @submit.prevent="onSubmit">

      <!-- General -->
    <div>
      <div class="flex items-center justify-between">
        <h4 className="section-title">General</h4>
        <ion-icon name="caret-up" @click="onFormToggle($event, 'general')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
      </div>
      <GeneralForm :contents="contents" :toggles="toggles" @update-contents="updateContents" />
    </div>

      <!-- Education -->

    <div>
      <div class="flex items-center justify-between">
        <h4 className="section-title">Education</h4>
        <ion-icon name="caret-up" class="cursor-pointer hover:text-gray-600 text-2xl" @click="onFormToggle($event, 'education')"></ion-icon>
      </div>
      <EducationForm :contents="contents" 
                      :toggles="toggles" 
                      @update-contents="updateContents"  
                      @delete-form="deleteForm" 
                      @add-form="addForm" />
    </div>

      <!-- Experience -->

    <div>
      <div class="flex items-center justify-between">
        <h4 className="section-title">Experience</h4>
        <ion-icon name="caret-up" @click="onFormToggle($event, 'experience')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
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

export default {
  name: 'CvForm',
  components: {
    GeneralForm,
    EducationForm,
    ExperienceForm,
  },
  props: {
    contents: Object
    },
  methods: {
    onSubmit(e) {
      e.preventDefault
    },
    updateContents(e, form){
      this.$emit('update-contents', e, form)
    },
    onFormToggle(e, form){
      const updated = this.toggles
      updated[form] = !updated[form]
      this.toggles = updated

      e.target.name === 'caret-up' ? 
      e.target.name = 'caret-down' : e.target.name = 'caret-up'
    },
    addForm(form){
      this.$emit('add-form', form)
    },
    deleteForm(form, id){
      this.$emit('delete-form', form, id)
    }
  },
  data(){
    return {
      toggles: {
        general: true,
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