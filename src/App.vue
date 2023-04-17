<template>
  <div>
    <CvForm @update-contents="updateContents" />
  </div>
</template>

<script>
import CvForm from './components/CvForm'

export default {
  name: 'App',
  components: {
    CvForm
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