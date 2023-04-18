<template>
  <div class="flex">
    <CvForm @update-contents="updateContents" />
    <CvDoc />
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
    updateContents(value){
      console.log(value)
    }
  },
  data(){
    return {
      contents: {
        name: '',
        email: '',
        phone: '',
        university: '',
        degree: '',
        from_uni: '',
        to_uni: '',
        company: '',
        position: '',
        description: '',
        from_comp: '',
        to_comp: ''
      }
    }
  }
}
</script>