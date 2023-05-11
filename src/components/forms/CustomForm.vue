<template>
    <div :id="section.title.toLowerCase() + '-' + section_index" v-if="section.toggle">
        <div class="sub-form">
            <div :key="index" v-for="(form, index) in section.forms">

                <div className="form-control">
                    <label htmlFor='title'>Title</label>
                    <input :id="section.title.toLowerCase() + '-title-' + index" 
                           :value='form.title' 
                           type='text' 
                           placeholder='Title' 
                           @input="onInput($event)" 
                    />
                </div>

                <div className="form-control">
                    <label htmlFor='subtitle'>Subtitle</label>
                    <input :id="section.title.toLowerCase() + '-subtitle-' + index" 
                           :value='form.subtitle' 
                           type='text' 
                           placeholder='Subtitle' 
                           @input="onInput($event)" 
                    />
                </div>

                <div className="form-control">
                    <label htmlFor='description'>Description</label>
                    <textarea :id="section.title.toLowerCase() + '-description-' + index"
                              :value='form.description' 
                              placeholder='Write a description for your custom section here...' 
                              @input="onInput($event)" 
                    />
                </div>

                <div className="form-control">
                    <label htmlFor='from'>From</label>
                    <input :id="section.title.toLowerCase() + '-from-' + index" 
                           :value='form.from' 
                           type='text'  
                           @input="onInput($event)" 
                    />
                </div>

                <div className="form-control">
                    <label htmlFor='to'>To</label>
                    <input :id="section.title.toLowerCase() + '-to-' + index" 
                           :value='form.to' 
                           type='text'
                           @input="onInput($event)" 
                    />
                </div>

                <div className="form-control">
                    <label htmlFor='link'>Link</label>
                    <input :id="section.title.toLowerCase() + '-link-' + index" 
                           :value='form.link' 
                           type='text'
                           placeholder='https://example.com' 
                           @input="onInput($event)" 
                    />
                </div>

                <hr v-if="section.forms[index] !== section.forms[section.forms.length - 1]" class="border border-[1.5px] rounded-md border-[#f1f4f6] my-8">
            </div>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CustomForm',
    props: {
      section: Object,
      section_index: Number
      },
    methods: {
      onInput(e){
        console.log(e.target.id)
      },
      onAddForm(form){
        this.$emit('add-form', form)
      },
      onDeleteForm(form, id){
        this.$emit('delete-form', form, id)
      }
    },
  }
  </script>