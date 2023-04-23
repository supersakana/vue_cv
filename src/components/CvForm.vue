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

        <div id="experience-form" v-if="toggles['experience']">
          <ion-icon name="add-circle" class="text-green-600 text-xl cursor-pointer" @click="onAddForm('experience')"></ion-icon>

          <div :key="exp.id" v-for="exp in contents.experience">
            <ion-icon name="remove-circle" class="text-red-600 text-xl cursor-pointer" @click="onDeleteForm('experience', exp.id)"></ion-icon>
            <div className="form-control">
              <label htmlFor='company'>Company</label>
              <input :id="'company-' + exp.id"
                     :data-id="exp.id" 
                     data-input="company" 
                     :value='exp.company' 
                     type='text' 
                     placeholder='Example Co' 
                     @input="onInput($event, 'experience')" 
                />
            </div>

            <div className="form-control">
              <label htmlFor='position'>Position</label>
              <input :id="'position-' + exp.id" 
                     :data-id="exp.id" 
                     data-input="position" 
                     :value='exp.position' 
                     type='text' 
                     placeholder='Position' 
                     @input="onInput($event, 'experience')" 
                />
            </div>

            <div className="form-control">
              <label htmlFor='company'>Description</label>
              <textarea :id="'description-' + exp.id"
                        :data-id="exp.id" 
                        data-input="description" 
                        :value='exp.description' 
                        placeholder='A description of your job here' 
                        @input="onInput($event, 'experience')" 
                  />
            </div>

            <div className="form-control">
              <label htmlFor='from_comp'>From</label>
              <input :id="'from-comp-' + exp.id"
                     :data-id="exp.id" 
                     data-input="from_comp" 
                     :value='exp.from_comp' 
                     type='date' 
                     @input="onInput($event, 'experience')" 
                />
            </div>

            <div className="form-control">
              <label htmlFor='to_comp'>To</label>
              <input :id="'to-comp-' + exp.id"
                     :data-id="exp.id"
                     data-input="to_comp" 
                     :value='exp.to_comp'  
                     type='date' 
                     @input="onInput($event, 'experience')" 
                />
            </div>
          </div>
        </div>
      </div>

      <input type='submit' value='Submit' className="bg-blue-500 text-white rounded-md py-1 px-2 hover:bg-blue-400 duration-500" />
    </form>
</template>

<script>
import GeneralForm from './forms/GeneralForm.vue'
import EducationForm from './forms/EducationForm.vue'

export default {
  name: 'CvForm',
  components: {
    GeneralForm,
    EducationForm,
  },
  props: {
    contents: Object
    },
  methods: {
    onSubmit(e) {
      e.preventDefault
    },
    onInput(e, form){
      this.$emit('update-contents', e, form)
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
    onAddForm(form){
      this.$emit('add-form', form)
    },
    addForm(form){
      this.$emit('add-form', form)
    },
    onDeleteForm(form, id){
      this.$emit('delete-form', form, id)
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