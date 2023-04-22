<template>
  <div class="flex">
    <CvForm :contents="contents" 
            @update-contents="updateContents" 
            @add-form="addForm"
            @delete-form="deleteForm"
      />
    <CvDoc :contents="contents" />
  </div>
</template>

<script>
import CvForm from './components/CvForm'
import CvDoc from './components/CvDoc.vue'

export default {
  name: 'App',
  components: {
    CvForm,
    CvDoc
  },
  methods: {
    updateContents(e, form){
      const updated = {...this.contents}
      const id = e.target.getAttribute('data-id')
      const input = e.target.getAttribute('data-input')
      
      if(form !== 'general'){
        updated[form].find((section) => section.id === id)[input] = e.target.value
      } else {
        updated[e.target.id] = e.target.value
      }
      this.contents = updated
    },
    addForm(form){
      const updated = {...this.contents}
      const id = (updated[form].length === 0) ?
        '0' : 
        `${parseInt(updated[form][updated[form].length - 1].id) + 1}`

      const newForm = (form === 'education') ?
        { id: id, university: 'Universtiy of Example', degree: 'Degree Title', from_uni: '2020-09-01', to_uni: '2020-09-01' } :
        { id: id, company: 'Company', position: 'Position Title', description: 'Write a description here of what you did', from_comp: '2020-09-01', to_comp: '2020-09-01' }

      updated[form] = [...updated[form], newForm]
      this.contents = updated
    },
    deleteForm(form, id){
      let updated = {...this.contents}
      updated[form] = updated[form].filter((f) => f.id !== id)
      this.contents = updated
    }
  },
  data(){
    return {
      contents: {
        name: 'John Doe',
        email: 'johndoe@example.com',
        phone: '+1 (234)-567-890',
        education: [
          {
            id: '0',
            university: 'University of Example',
            degree: 'Degree Title',
            from_uni: '2020-09-01',
            to_uni: '2020-09-01',
          }
        ],
        experience: [
          {
            id: '0',
            company: 'Company',
            position: 'Position Title',
            description: 'Write a simple description here of what you did',
            from_comp: '2020-09-01',
            to_comp: '2020-09-01'
          },
        ],
      }
    }
  }
}
</script>