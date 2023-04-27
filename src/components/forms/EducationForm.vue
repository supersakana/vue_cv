<template>
  <div id="education-form" v-if="toggles['education']">
    <div class="sub-form">
      <ion-icon name="add-circle" class="text-green-600 text-xl cursor-pointer" @click="onAddForm('education')"></ion-icon>
      <div :key="edu.id" v-for="edu in contents.education">
        <ion-icon name="remove-circle" class="text-red-600 text-xl cursor-pointer" @click="onDeleteForm('education', edu.id)"></ion-icon>
        <div className="form-control">
          <label htmlFor='university'>University</label>
          <input :id="'university-' + edu.id"
                :data-id="edu.id" 
                data-input="university" 
                :value='edu.university' 
                type='text'
                placeholder='University of Example'
                @input="onInput($event, 'education')" 
              />
        </div>

        <div className="form-control">
          <label htmlFor='degree'>Degree</label>
          <input :id="'degree-' + edu.id" 
                :data-id="edu.id" 
                data-input="degree" 
                :value='edu.degree' 
                type='text' 
                placeholder='BS in Example Science' 
                @input="onInput($event, 'education')" 
              />
        </div>

        <div className="form-control">
          <label htmlFor='from_uni'>From</label>
          <input :id="'from-uni-' + edu.id"
                :data-id="edu.id"
                data-input="from_uni"
                :value='edu.from_uni' 
                type='date' 
                @input="onInput($event, 'education')" 
              />
        </div>

        <div className="form-control">
          <label htmlFor='to_uni'>To</label>
          <input :id="'to-uni-' + edu.id"
                  :data-id="edu.id" 
                  data-input="to_uni" 
                  :value='edu.to_uni' 
                  type='date' 
                  @input="onInput($event, 'education')"
              />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EducationForm',
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