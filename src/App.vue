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