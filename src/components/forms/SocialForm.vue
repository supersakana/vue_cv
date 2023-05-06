<template>
    <div id="general-form" v-if="toggles['social']">
      <div class="sub-form">
        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91]" name="logo-linkedin"></ion-icon>
            <label htmlFor='linkedin'>LinkedIn</label>
          </div>
          <input id='linkedin' 
                type='text' 
                placeholder="https://linkedin.com/username"  
                @input="onInput($event, 'social')" 
            />
        </div>

        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91]" name="logo-twitter"></ion-icon>
            <label htmlFor='twitter'>Twitter</label>
          </div>
          <input id='twitter' 
                type='text' 
                placeholder="https://twitter.com/username"  
                @input="onInput($event, 'social')" 
            />
        </div>

        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91]" name="logo-github"></ion-icon>
            <label htmlFor='github'>GitHub</label>
          </div>
          <input id='github' 
                type='text' 
                placeholder="https://github.com/username"  
                @input="onInput($event, 'social')" 
            />
        </div>

        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91]" name="logo-instagram"></ion-icon>
            <label htmlFor='instagram'>Instagram</label>
          </div>
          <input id='instagram' 
                type='text' 
                placeholder="https://instagram.com/username"  
                @input="onInput($event, 'social')" 
            />
        </div>

        <div className="form-control">
          <div class="flex items-center gap-x-1">
            <ion-icon class="text-[#566f91]" name="logo-facebook"></ion-icon>
            <label htmlFor='facebook'>Facebook</label>
          </div>
          <input id='facebook' 
                type='text' 
                placeholder="https://facebook.com/username"  
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