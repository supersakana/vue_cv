<template>
  <div class="flex">
    <CvForm @update-contents="updateContents" />
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
    updateContents(e){
      const updated = {...this.contents}
      updated[e.target.id] = e.target.value

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
            id: 1,
            university: 'Universtiy of Example',
            degree: 'Degree Title',
            from_uni: '2020-09-01',
            to_uni: '2020-09-01',
          }
        ],
        experience: [
          {
            id: 1,
            company: 'Company Title',
            position: 'Position Title',
            description: 'Write a simple description here of what you did',
            from_comp: '2020-09-01',
            to_comp: '2020-09-01'
          }
        ],
      }
    }
  }
}
</script>