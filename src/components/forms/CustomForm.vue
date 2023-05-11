<template>
    <div :id="section.title.toLowerCase() + '-' + section_index" v-if="section.toggle">
        <div class="sub-form">
            <div :key="index" v-for="(form, index) in section.forms">

                <div className="form-control">
                    <label htmlFor='title'>Header</label>
                    <input :id="section.title.toLowerCase() + '-header-' + index" 
                           :value='form.header' 
                           type='text' 
                           placeholder='Header' 
                           @input="onInput($event, form, 'header')" 
                    />
                </div>

                <div className="form-control">
                    <label htmlFor='description'>Description</label>
                    <textarea :id="section.title.toLowerCase() + '-description-' + index"
                              :value='form.description' 
                              placeholder='Write a description for your custom section here...' 
                              @input="onInput($event, form, 'description')" 
                    />
                </div>

                <div className="form-control">
                    <label htmlFor='from'>From</label>
                    <input :id="section.title.toLowerCase() + '-from-' + index" 
                           :value='form.from' 
                           type='text'  
                           @input="onInput($event, form, 'from')" 
                    />
                </div>

                <div className="form-control">
                    <label htmlFor='to'>To</label>
                    <input :id="section.title.toLowerCase() + '-to-' + index" 
                           :value='form.to' 
                           type='text'
                           @input="onInput($event, form, 'to')" 
                    />
                </div>

                <div className="form-control">
                    <label htmlFor='link'>Link</label>
                    <input :id="section.title.toLowerCase() + '-link-' + index" 
                           :value='form.link' 
                           type='text'
                           placeholder='https://example.com' 
                           @input="onInput($event, form, 'link')" 
                    />
                </div>

                <hr v-if="section.forms[index] !== section.forms[section.forms.length - 1]" class="border border-[1.5px] rounded-md border-[#f1f4f6] my-8">
            </div>
            <button class="button-bg my-3 px-4 py-2 font-bold text-white rounded-lg duration-500"  @click="onAddForm($event)">Add {{ singularize(section.title) }}</button>
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
      onInput(e, form, input){
        const updated = form
        updated[input] = e.target.value
        form = updated
      },
      onAddForm(e){
        console.log(e)
        // this.$emit('add-form', form)
      },
      onDeleteForm(form, id){
        this.$emit('delete-form', form, id)
      },

      // https://stackoverflow.com/questions/57429677/javascript-make-a-word-singular-singularize
      singularize(word) {
        const endings = {
            ves: 'fe',
            ies: 'y',
            i: 'us',
            zes: 'ze',
            ses: 's',
            es: 'e',
            s: ''
        };
        if(word === ''){
            return 'Form'
        } else {
            return word.replace(
            new RegExp(`(${Object.keys(endings).join('|')})$`), 
            r => endings[r]
            );  
        }
      }
    },
  }
  </script>