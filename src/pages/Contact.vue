<template>
  <Layout>
    <div class="container">

      <div class="contact-header">
        <h1 class="contact-title">Say hi!</h1>
        <p>Leave me a note with any questions you might have, I'll get back to you as soon as possible.</p>
      </div>

      <form class="contact-form" name="contact" @submit.prevent="submitForm">

        <div class="sender-info">
          <div>
            <label for="name" class="label">Your name</label>
            <input v-model="formData.name" type="text" name="name" />
          </div>
          <div>
            <label for="email" class="label">Your email</label>
            <input v-model="formData.email" type="email" name="email" />
          </div>
        </div>

        <div class="message">
          <label for="message" class="label">Message</label>
          <textarea v-model="formData.message" name="message"></textarea>
        </div>

        <button class="button">Submit form</button>

      </form>

    </div>
  </Layout>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Contact',
  data () {
    return {      
      initFormData: {
        name: '',
        email: '',
        message: ''
      },
      formData: null
    }
  },
  created() {
    this.initFormDataFn()
  },
  methods: {
      initFormDataFn () {
        this.formData = JSON.parse(JSON.stringify(this.initFormData))
      },
      async submitForm () {
        try {    
          await axios.post(`${this.GRIDSOME_API_URL}/contacts`, this.formData)
          this.initFormDataFn()
          alert('提交成功')
        } catch (err) {      
          console.log(err);
          alert('提交失败！请稍后再试')
        }
      }
  },
}
</script>

<style scoped>
.contact-header {
  padding: 2rem 0 4rem 0;
}
.contact-title {
  font-size: 4rem;
  margin: 0 0 4rem 0;
  padding: 0;
}
.sender-info {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 2rem;
}
.sender-info > div {
  flex: 1;
  margin-right: 4rem;
}
.sender-info > div:last-of-type {
  margin: 0;
}
input:focus,textarea:focus {
  border-color: var(--color-contrast-1);
}
input,textarea {
  background: transparent;
  border: 1px solid var(--color-base-1);
  outline: none;
  border-radius: 0.3rem;
  padding: 0.8rem 1rem;
  color: inherit;
  font-size: 1rem;
  width: 100%;
}
textarea {
  resize: none;
  height: 140px;
}
.button {
  color: var(--color-base);
  background: var(--color-contrast);
  outline: none;
  border: 0;
  font-size: 0.8rem;
  padding: 0.8rem 1.6rem;
  border-radius: 0.3rem;
  margin-top: 2rem;
  cursor: pointer;
  transition: opacity 0.25s ease;
  font-size: 500;
  letter-spacing: 0.035em;
}
.button:hover {
  opacity: 0.6;
}
.button:focus {
  border: 1px solid var(--color-base-1);
}
</style>

