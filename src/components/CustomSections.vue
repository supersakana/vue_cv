<template>
  <div id="custom-form">
    <div>
      <div :key="index" v-for="(section, index) in contents.custom">
        <div class="mx-4 my-2">
          <div class="flex items-center">
              <ion-icon name="chevron-down-outline" class="cursor-pointer hover:text-gray-600 text-2xl" @click="onSectionToggle($event, section)"></ion-icon>
              <h4 className="section-title">{{ section.title }}</h4>
          </div>
          <CustomForm :section="section"
                      :index="index" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CustomForm from './forms/CustomForm.vue'
export default {
  name: 'CustomSections',
  components: {
    CustomForm
  },
  props: {
    contents: Object
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
    },
    onSectionToggle(e, section){
      // console.log(index, e.target.name, section)
      const updated = section
      updated.toggle = !updated.toggle
      section = updated

      e.target.name === 'chevron-down-outline' ? 
      e.target.name = 'chevron-up-outline' : e.target.name = 'chevron-down-outline'
    },
  },
}
</script>