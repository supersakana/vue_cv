<template>
  <div id="general-form" v-if="toggles['general']">
    <div className="form-control">
      <label htmlFor='name'>Name</label>
      <input id='name' 
             type='text' 
             placeholder="John Doe" 
             :value='contents.name' 
             @input="onInput($event, 'general')" 
        />
    </div>

    <div className="form-control">
      <label htmlFor='email'>Email</label>
      <input id='email'
             type='email' 
             placeholder='example@this.com' 
             :value='contents.email' 
             @input="onInput($event, 'general')" 
        />
    </div>

    <div className="form-control">
      <label htmlFor='phone'>Phone</label>
      <input id='phone'  
             type='phone' 
             placeholder='+1 (123)-456-789'
             :value='contents.phone'
             @input="onInput($event, 'general')" 
        />
    </div>
  </div>
</template>

<script>
export default {
  name: 'GeneralForm',
  props: {
    contents: Object,
    toggles: Object
    },
  methods: {
    onInput(e, form){
      this.$emit('update-contents', e, form)
    },
  },
}
</script>