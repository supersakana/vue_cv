<template>
    <div id="general-form" v-if="toggles['social']">
      <div class="sub-form dark:border-[#364150]">
        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91] dark:text-gray-300" name="logo-linkedin"></ion-icon>
            <label class="dark:text-gray-300" htmlFor='linkedin'>LinkedIn</label>
          </div>
          <input id='linkedin' 
                 class="dark:bg-[#171e25] dark:text-white"
                 type='text' 
                 placeholder="https://linkedin.com/username"
                 :value='contents.linkedin'
                 @input="onInput($event, 'social')" 
            />
        </div>

        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91] dark:text-gray-300" name="logo-twitter"></ion-icon>
            <label class="dark:text-gray-300" htmlFor='twitter'>Twitter</label>
          </div>
          <input id='twitter'
                 class="dark:bg-[#171e25] dark:text-white"
                 type='text' 
                 placeholder="https://twitter.com/username"
                 :value='contents.twitter'
                 @input="onInput($event, 'social')" 
            />
        </div>

        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91] dark:text-gray-300" name="logo-github"></ion-icon>
            <label class="dark:text-gray-300" htmlFor='github'>GitHub</label>
          </div>
          <input id='github' 
                 class="dark:bg-[#171e25] dark:text-white"
                 type='text' 
                 placeholder="https://github.com/username"  
                 :value='contents.github'
                 @input="onInput($event, 'social')" 
            />
        </div>

        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91] dark:text-gray-300" name="logo-instagram"></ion-icon>
            <label class="dark:text-gray-300" htmlFor='instagram'>Instagram</label>
          </div>
          <input id='instagram' 
                 class="dark:bg-[#171e25] dark:text-white"
                 type='text'
                 placeholder="https://instagram.com/username"
                 :value='contents.instagram'
                 @input="onInput($event, 'social')" 
            />
        </div>

        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91] dark:text-gray-300" name="logo-facebook"></ion-icon>
            <label class="dark:text-gray-300" htmlFor='facebook'>Facebook</label>
          </div>
          <input id='facebook'
                 class="dark:bg-[#171e25] dark:text-white"
                 type='text' 
                 placeholder="https://facebook.com/username"
                 :value='contents.facebook'
                 @input="onInput($event, 'social')" 
            />
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'SocialForm',
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