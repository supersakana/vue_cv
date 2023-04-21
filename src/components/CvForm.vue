<template>
  <form @submit.prevent="onSubmit">

      <!-- General -->

      <div>
        <div class="flex items-center justify-between">
          <h4 className="section-title">General</h4>
          <ion-icon name="caret-up" @click="onFormToggle($event, 'general')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
        </div>

        <div id="general-form" v-if="toggles['general']">
          <div className="form-control">
            <label htmlFor='name'>Name</label>
            <input id='name' :value='contents.name' type='text' placeholder="John Doe" @input="onInput" />
          </div>

          <div className="form-control">
            <label htmlFor='email'>Email</label>
            <input id='email' :value='contents.email' type='email' placeholder='example@this.com' @input="onInput" />
          </div>

          <div className="form-control">
            <label htmlFor='phone'>Phone</label>
            <input id='phone' :value='contents.phone' type='phone' placeholder='+1 (123)-456-789' @input="onInput" />
          </div>
        </div>
      </div>

      <!-- Education -->

      <div>
        <div class="flex items-center justify-between">
          <h4 className="section-title">Education</h4>
          <ion-icon name="caret-up" @click="onFormToggle($event, 'education')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
        </div>

        <div id="education-form" v-if="toggles['education']">
          <div :key="edu.id" v-for="edu in contents.education">

            <div className="form-control">
              <label htmlFor='university'>University</label>
              <input :id="'university-' + edu.id" :value='edu.university' type='text' placeholder='University of Example' @input="onInput($event, 'education')" />
            </div>

            <div className="form-control">
              <label htmlFor='degree'>Degree</label>
              <input :id="'degree-' + edu.id" :value='edu.degree' type='text' placeholder='BS in Example Science' @input="onInput($event, 'education')" />
            </div>

            <div className="form-control">
              <label htmlFor='from_uni'>From</label>
              <input :id="'from-uni-' + edu.id" :value='edu.from_uni' type='date' @input="onInput($event, 'education')" />
            </div>

            <div className="form-control">
              <label htmlFor='to_uni'>To</label>
              <input :id="'to-uni-' + edu.id" :value='edu.to_uni' type='date' @input="onInput($event, 'education')" />
            </div>
            
          </div>
        </div>
      </div>

      <!-- Experience -->

      <div>
        <div class="flex items-center justify-between">
          <h4 className="section-title">Experience</h4>
          <ion-icon name="caret-up" @click="onFormToggle($event, 'experience')" class="cursor-pointer hover:text-gray-600 text-2xl"></ion-icon>
        </div>

        <div id="experience-form" v-if="toggles['experience']">
          <div :key="exp.id" v-for="exp in contents.experience">

            <div className="form-control">
              <label htmlFor='company'>Company</label>
              <input :id="'company-' + exp.id" :value='exp.company' type='text' placeholder='Example Co' @input="onInput($event, 'experience')" />
            </div>

            <div className="form-control">
              <label htmlFor='position'>Position</label>
              <input :id="'position-' + exp.id" :value='exp.position' type='text' placeholder='Position' @input="onInput($event, 'experience')" />
            </div>

            <div className="form-control">
              <label htmlFor='company'>Description</label>
              <textarea :id="'description-' + exp.id" :value='exp.description' placeholder='A description of your job here' @input="onInput($event, 'experience')" />
            </div>

            <div className="form-control">
              <label htmlFor='from_comp'>From</label>
              <input :id="'from-comp-' + exp.id" :value='exp.from_comp' type='date' @input="onInput($event, 'experience')" />
            </div>

            <div className="form-control">
              <label htmlFor='to_comp'>To</label>
              <input :id="'to-comp-' + exp.id" :value='exp.to_comp'  type='date' @input="onInput($event, 'experience')" />
            </div>
            
          </div>
        </div>
      </div>

      <input type='submit' value='Submit' className="bg-blue-500 text-white rounded-md py-1 px-2 hover:bg-blue-400 duration-500" />
    </form>
</template>

<script>
export default {
  name: 'CvForm',
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
    onFormToggle(e, form){
      const updated = this.toggles
      updated[form] = !updated[form]
      this.toggles = updated

      e.target.name === 'caret-up' ? 
      e.target.name = 'caret-down' : e.target.name = 'caret-up'
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
.form-control{
  display: flex;
  gap: 5px;
  margin-top: 2px;
}

.section-title{
  font-weight: bold;
  font-size: 1.5rem;
}
</style>