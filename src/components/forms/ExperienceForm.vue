<template>
  <div id="experience-form" v-if="toggles['experience']">
    <div class="sub-form">
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
      <button class="button-bg mb-3 mt-1 px-4 py-2 font-bold text-white rounded-lg duration-500"  @click="onAddForm('experience')">Add Experience</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ExperienceForm',
  props: {
    contents: Object,
    toggles: Object
    },
  methods: {
    onInput(e, form){
      this.$emit('update-contents', e, form)
    },
    onAddForm(form){
      this.$emit('add-form', form)
    },
    onDeleteForm(form, id){
      this.$emit('delete-form', form, id)
    }
  },
}
</script>