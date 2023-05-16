<template>
  <div id="custom-form">
    <div>
      <div :key="index" v-for="(section, index) in contents.custom">
        <div class="mx-4 my-2">

          <!-- Chevron title section -->
          <div class="flex justify-between">
            <div class="flex items-center">
                <ion-icon name="chevron-down-outline" class="cursor-pointer hover:text-gray-600 text-2xl dark:text-white" @click="onSectionToggle($event, section)"></ion-icon>
                <h4 class="section-title dark:text-white">{{ section.title === '' ?  `Section ${index + 1}` : section.title }}</h4>
            </div>

            <SectionSlider />
          </div>

          <!-- Section title input -->
          <div :id="section.title.toLowerCase() + '-section'" v-if="section.toggle">
            <div class="form-control">
              <div class="flex justify-between">
                <label class="dark:text-gray-300" :htmlFor="'section-title-' + index">Section Title</label>
                <span class="text-gray-400 hover:text-red-500 cursor-pointer underline text-gray-300" @click="onSectionDelete(contents, index)">Remove Section</span>
              </div>

              <input :id="section.title.toLowerCase() + '-title'"
                        :value='section.title' 
                        class="my-2 dark:bg-[#171e25] dark:text-white"
                        type='text'
                        placeholder='Section Title'
                        @input="onInput($event, section)" 
                      />
            </div>

            <!-- Loop thorugh each subform -->
            <CustomForm :section="section"
                        :section_index="index" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CustomForm from './forms/CustomForm.vue'
import SectionSlider from './SectionSlider.vue'

export default {
  name: 'CustomSections',
  components: {
    CustomForm,
    SectionSlider
  },
  props: {
    contents: Object
    },
  methods: {
    onInput(e, section){
        const updated = section
        updated.title = e.target.value
        section = updated
      },
    onAddForm(form){
      this.$emit('add-form', form)
    },
    onDeleteForm(form, id){
      this.$emit('delete-form', form, id)
    },
    onSectionToggle(e, section){
      const updated = section
      updated.toggle = !updated.toggle
      section = updated

      e.target.name === 'chevron-down-outline' ? 
      e.target.name = 'chevron-up-outline' : e.target.name = 'chevron-down-outline'
    },
    onSectionDelete(contents, index){
      const updated = contents
      updated.custom = updated.custom.filter((_section, i) => i !== index)
      contents = updated
    }
  },
}
</script>