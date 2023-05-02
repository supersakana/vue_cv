<template>
  <div id="education-form" v-if="toggles['education']">
    <div class="sub-form">
      <div :key="edu.id" v-for="edu in contents.education">
        
        <div className="form-control">
          <div class="flex items-center justify-between">
            <label htmlFor='university'>University</label>
            <ion-icon name="close-circle" class="text-gray-300 hover:text-red-500 text-xl cursor-pointer ml-[14px] min-w-[16px] min-h-[16px]" @click="onDeleteForm('education', edu.id)"></ion-icon>
          </div>
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
      <button class="button-bg mb-3 mt-1 px-4 py-2 font-bold text-white rounded-lg duration-500"  @click="onAddForm('education')">Add School</button>
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