<template>
  <div id="general-form" v-if="toggles['general']">
    <div class="sub-form dark:border-[#364150]">
      <div className="form-control">
        <label class="dark:text-gray-300" htmlFor='name'>Name</label>
        <input id='name'
              class="dark:bg-[#171e25] dark:text-white"
              type='text' 
              placeholder="John Doe" 
              :value='contents.name' 
              @input="onInput($event, 'general')" 
          />
      </div>

      <div className="form-control">
        <label class="dark:text-gray-300" htmlFor='email'>Email</label>
        <input id='email'
              class="dark:bg-[#171e25] dark:text-white"
              type='email' 
              placeholder='example@this.com' 
              :value='contents.email' 
              @input="onInput($event, 'general')" 
          />
      </div>

      <div className="form-control">
        <label class="dark:text-gray-300" htmlFor='phone'>Phone</label>
        <input id='phone'  
               class="dark:bg-[#171e25] dark:text-white"
               type='phone' 
               placeholder='+1 (123)-456-789'
               :value='contents.phone'
               @input="onInput($event, 'general')" 
          />
      </div>

      <div className="form-control">
        <label class="dark:text-gray-300" htmlFor='location'>Location</label>
        <input id='location'
              class="dark:bg-[#171e25] dark:text-white"
              type='text' 
              placeholder='1800 Example St' 
              :value='contents.location' 
              @input="onInput($event, 'general')" 
          />
      </div>

      <div className="form-control">
        <label class="dark:text-gray-300" htmlFor='bio'>Bio</label>
        <textarea id='bio'
                  class="dark:bg-[#171e25] dark:text-white"
                  type='text' 
                  placeholder='Tell us about yourself...' 
                  :value='contents.bio'
                  @input="onInput($event, 'general')" 
          />
      </div>
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