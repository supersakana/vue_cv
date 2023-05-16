<template>
  <div class="flex">
    <ion-icon id="dark-mode" class="absolute right-0 text-3xl my-6 mx-5 text-[#404040] cursor-pointer dark:hover:text-white opacity-50 hover:opacity-100 duration-500 z-1" name="moon" @click="darkModeToggle($event)"></ion-icon>

    <div class="w-full md:max-w-[450px] font-poppins border-r bg-white dark:bg-[#0b1115] dark:border-none duration-500">
      <CvForm :contents="contents" 
              @update-contents="updateContents" 
              @add-form="addForm"
              @delete-form="deleteForm"
              @add-skill="addSkill"
              @delete-skill="deleteSkill"
              @export-pdf="exportPDF"
              @add-section="addSection" />
    </div>
    
    <div id="cv-doc" class="w-full hidden md:block justify-center bg-no-repeat bg-cover bg-pattern dark:bg-pattern-dark h-screen overflow-y-scroll py-20 duration-500">
      <button class="button-bg px-4 py-2 font-bold text-white rounded-3xl duration-500 block mx-auto mb-5 mt-[-15px]" @click="exportPDF">Download PDF</button>
      <div ref="document" class="shadow-lg p-3 m-3 w-[8in] h-[10.5in] bg-white p-[24px] font-roboto m-auto">
        <CvDoc :contents="contents" />
      </div>
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
      university: 'University of Example',
      degree: 'Degree Title',
      from_uni: 'September 2018',
      to_uni: 'May 2022',
    },
    experience: {
      id: id,
      company: 'Company',
      position: 'Position Title',
      description: 'Write a simple description here of what you did',
      from_comp: 'September 2018',
      to_comp: 'May 2022'
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
      const id = e.target.getAttribute('data-id')
      const input = e.target.getAttribute('data-input')
      
      if(form === 'general' || form === 'social'){     
        updated[e.target.id] = e.target.value 
      } else if (form === 'skills'){
        updated['skills'][id] = e.target.value
      } else {
        updated[form].find((section) => section.id === id)[input] = e.target.value
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
    addSection(){
      let updated = {...this.contents}
      const newSection = {
            title: '',
            toggle: true,
            forms:[
              {
                header: '',
                description: '',
                from: '',
                to: '',
                link: ''
              },
            ]
          }

      updated['custom'] = [...updated['custom'], newSection]
      this.contents = updated
    },
    darkModeToggle(e){
      const btn = document.querySelector('#dark-mode')

      if(e.target.name === 'moon'){
            e.target.name = 'sunny';
            document.documentElement.classList.add('dark')
            localStorage.theme = 'dark'

            btn.classList.remove('text-[#404040]')
            btn.classList.add('text-white')
        } else {
            e.target.name = 'moon';
            document.documentElement.classList.remove('dark')
            localStorage.theme = 'light'

            btn.classList.remove('text-white')
            btn.classList.add('text-[#404040]')
        }
    },
    exportPDF(){
      // https://stackoverflow.com/questions/60204249/cannnot-convert-html-code-to-pdf-with-vue-html2pdf
      // https://stackoverflow.com/questions/69705309/jspdf-html2canvas-losing-spaces-and-misaligning-text-generally
      html2pdf(this.$refs.document, {
					margin: 0.05,
					filename: 'document.pdf',
					image: { type: 'jpeg', quality: 1 },
					html2canvas: { dpi: 192, letterRendering: true, scale: 2 },
					jsPDF: { unit: 'in', format: 'letter', orientation: 'portrait' }
				})
    }
  },
  data(){
    return {
      contents: {
        name: 'John Doe',
        email: 'johndoe@example.com',
        phone: '+1 (234)-567-890',
        location: 'Virginia Beach, VA',
        bio: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Fusce ut placerat orci nulla pellentesque.',
        linkedin: '',
        twitter: '',
        github: '',
        instagram: '',
        facebook: '',
        skills: ['HTML', 'CSS', 'JavaScript', 'Ruby', 'Ruby on Rails', 'RSpec', 'WordPress', 'Divi', 'Elementor', 'Vue', 'Tailwind', 'Git', 'GitHub'],
        education: [defaults('education', '0')],
        experience: [defaults('experience', '0')],
        custom: []
      },
      sliders: ['skills', 'education', 'experience']
    }
  },
}
</script>

<style>
  *,
  *::before,
  *::after {
    letter-spacing: 0.01px;
  }

  body,
  html {
    width: 100%;
  }

</style>