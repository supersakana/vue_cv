<template>
  <form @submit.prevent="onSubmit">
      <h4 className="section-title">General</h4>

      <div className="form-control">
        <label htmlFor='name'>Name</label>
        <input id='name' type='text' placeholder="John Doe" @input="onInput" />
      </div>

      <div className="form-control">
        <label htmlFor='email'>Email</label>
        <input id='email' type='email' placeholder='example@this.com' @input="onInput" />
      </div>

      <div className="form-control">
        <label htmlFor='phone'>Phone</label>
        <input id='phone' type='phone' placeholder='+1 (123)-456-789' @input="onInput" />
      </div>

      <h4 className="section-title">Education</h4>

      <div className="form-control">
        <label htmlFor='university'>University</label>
        <input id='university' type='text' placeholder='University of Example' @input="onInput" />
      </div>

      <div className="form-control">
        <label htmlFor='degree'>Degree</label>
        <input id='degree' type='text' placeholder='Degree Title' @input="onInput" />
      </div>

      <div className="form-control">
        <label htmlFor='from_uni'>From</label>
        <input id='from_uni' type='date' @input="onInput" />
      </div>

      <div className="form-control">
        <label htmlFor='to_uni'>To</label>
        <input id='to_uni' type='date' @input="onInput" />
      </div>

      <h4 className="section-title">Experience</h4>

      <div className="form-control">
        <label htmlFor='company'>Company</label>
        <input id='company' type='text' placeholder='Company Name' @input="onInput" />
      </div>

       <div className="form-control">
        <label htmlFor='position'>Position</label>
        <input id='position' type='text' placeholder='Position Title' @input="onInput" />
      </div>

      <div className="form-control">
        <label htmlFor='company'>Description</label>
        <textarea id='description' placeholder='A description of your job here' @input="onInput" />
      </div>

      <div className="form-control">
        <label htmlFor='from_comp'>From</label>
        <input id='from_comp' type='date' @input="onInput" />
      </div>

      <div className="form-control">
        <label htmlFor='to_comp'>To</label>
        <input id='to_comp' type='date' @input="onInput" />
      </div>

      <input type='submit' value='Submit' className="bg-blue-500 text-white rounded-md py-1 px-2 hover:bg-blue-400 duration-500" />
    </form>
</template>

<script>
export default {
  name: 'CvForm',
  methods: {
    onSubmit(e) {
      e.preventDefault
    },
    onInput(e){
      this.$emit('update-contents', e.target.value)
    }
  }
}
</script>

<style>
.form-control{
  display: flex;
  gap: 5px;
  margin-top: 2px;
}

.section-title{
  font-weight: bold;
  font-size: 1.5rem;
}
</style>