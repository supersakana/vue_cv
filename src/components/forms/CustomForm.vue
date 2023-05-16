<template>
    <div :id="section.title.toLowerCase() + '-' + section_index" v-if="section.toggle">
        <div class="sub-form dark:border-[#364150]">
            <div :key="index" v-for="(form, index) in section.forms">

                <div className="form-control">
                    <div class="flex items-center justify-between">
                        <label class="dark:text-gray-300" htmlFor='title'>Header</label>
                        <ion-icon name="close-circle" class="text-2xl text-gray-300 hover:text-red-500 text-xl cursor-pointer ml-[14px] min-w-[20px] min-h-[20px]" @click="onDeleteForm(section, index)"></ion-icon>
                    </div>
            
                    <input :id="section.title.toLowerCase() + '-header-' + index" 
                           class="dark:bg-[#171e25] dark:text-white"
                           :value='form.header' 
                           type='text' 
                           placeholder='Header' 
                           @input="onInput($event, form, 'header')" 
                    />
                </div>

                <div className="form-control">
                    <label class="dark:text-gray-300" htmlFor='description'>Description</label>
                    <textarea :id="section.title.toLowerCase() + '-description-' + index"
                              class="dark:bg-[#171e25] dark:text-white"
                              :value='form.description' 
                              placeholder='Write a description for your custom section here...' 
                              @input="onInput($event, form, 'description')" 
                    />
                </div>

                <div className="form-control">
                    <label class="dark:text-gray-300" htmlFor='from'>From</label>
                    <input :id="section.title.toLowerCase() + '-from-' + index"
                           class="dark:bg-[#171e25] dark:text-white"
                           :value='form.from' 
                           type='text'  
                           @input="onInput($event, form, 'from')" 
                    />
                </div>

                <div className="form-control">
                    <label class="dark:text-gray-300" htmlFor='to'>To</label>
                    <input :id="section.title.toLowerCase() + '-to-' + index" 
                           class="dark:bg-[#171e25] dark:text-white"
                           :value='form.to' 
                           type='text'
                           @input="onInput($event, form, 'to')" 
                    />
                </div>

                <div className="form-control">
                    <label class="dark:text-gray-300" htmlFor='link'>Link</label>
                    <input :id="section.title.toLowerCase() + '-link-' + index"
                           class="dark:bg-[#171e25] dark:text-white"
                           :value='form.link' 
                           type='text'
                           placeholder='https://example.com' 
                           @input="onInput($event, form, 'link')" 
                    />
                </div>

                <hr v-if="section.forms[index] !== section.forms[section.forms.length - 1]" class="border border-[1.5px] rounded-md border-[#f1f4f6] my-8">
            </div>
            <button class="button-bg my-3 px-4 py-2 font-bold text-white rounded-lg duration-500"  @click="onAddForm(section)">Add {{ singularize(section.title) }}</button>
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
      onAddForm(section){
        const updated = section
        const newForm = {
            header: '',
            description: '',
            from: '',
            to: '',
            link: ''
        }

        updated['forms'] = [...updated['forms'], newForm]
        section = updated
      },
      onDeleteForm(section, index){
        let updated = section
        updated.forms = updated.forms.filter((_form, i) => i !== index)
        section = updated
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