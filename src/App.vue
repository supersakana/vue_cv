<template>
  <div class="flex">
    <CvForm :contents="contents" 
            @update-contents="updateContents" 
            @add-form="addForm"
            @delete-form="deleteForm"
            @add-skill="addSkill"
            @delete-skill="deleteSkill"
            @export-pdf="exportPDF"
      />
    <div id="cv-doc" ref="document">
      <CvDoc :contents="contents" />
    </div>
  </div>
</template>

<script>
import CvForm from './components/CvForm'
import CvDoc from './components/CvDoc.vue'
import html2pdf from 'html2pdf.js'

function defaults(form, id){
  const data = {
    education: {
      id: id,
      university: 'University of Virginia',
      degree: 'Degree Title',
      from_uni: '2020-09-01',
      to_uni: '2020-09-01',
    },
    experience: {
      id: id,
      company: 'Company',
      position: 'Position Title',
      description: 'Write a simple description here of what you did',
      from_comp: '2020-09-01',
      to_comp: '2020-09-01'
    }
  }
  return data[form]
}

export default {
  name: 'App',
  components: {
    CvForm,
    CvDoc,
  },
  methods: {
    updateContents(e, form){
      const updated = {...this.contents}
      
      if(form !== 'general'){
        const id = e.target.getAttribute('data-id')
        const input = e.target.getAttribute('data-input')
        
        updated[form].find((section) => section.id === id)[input] = e.target.value
      } else {
        updated[e.target.id] = e.target.value
      }
      this.contents = updated
    },
    addForm(form){
      const updated = {...this.contents}
      const id = (updated[form].length === 0) ?
        '0' : `${parseInt(updated[form][updated[form].length - 1].id) + 1}`

      const newForm = defaults(form, id)

      updated[form] = [...updated[form], newForm]
      this.contents = updated
    },
    deleteForm(form, id){
      let updated = {...this.contents}
      updated[form] = updated[form].filter((f) => f.id !== id)
      this.contents = updated
    },
    addSkill(skill){
      let updated = {...this.contents}
      updated['skills'] = [...updated['skills'], skill]
      this.contents = updated
    },
    deleteSkill(index){
      let updated = {...this.contents}
      updated['skills'] = updated['skills'].filter((_skill, i) => i !== index)
      this.contents = updated
    },
    exportPDF(){
      html2pdf(this.$refs.document, {
					margin: 1,
					filename: 'document.pdf',
					image: { type: 'jpeg', quality: 0.98 },
					html2canvas: { dpi: 192, letterRendering: true },
					jsPDF: { unit: 'in', format: 'letter', orientation: 'landscape' }
				})
    }
  },
  data(){
    return {
      contents: {
        name: 'John Doe',
        email: 'johndoe@example.com',
        phone: '+1 (234)-567-890',
        location: '1800 Example St',
        bio: 'Tell us about yourself...',
        skills: ['HTML', 'CSS', 'JavaScript'],
        education: [defaults('education', '0')],
        experience: [defaults('experience', '0')]
      }
    }
  }
}
</script>

<style>
  * {
    letter-spacing: 0.01px;
  }
</style>