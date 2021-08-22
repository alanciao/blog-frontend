<template>
  <Layout>
    <div class="container">
      <div class="contact-header">
        <h1 class="contact-title">Say hi!</h1>
        <p>Leave me a note with any questions you might have, I'll get back to you as soon as possible.</p>
      </div>
      <form name="contact" class="contact-form">
        <div class="sender-info">
          <div>
            <label for="name" class="label">Your name</label>
            <input type="text" name="name" v-model="form.name">
          </div>
          <div>
            <label for="email" class="label">Your email</label>
            <input type="email" name="email" v-model="form.email">
          </div>
        </div>
        <div class="message">
          <label for="message" class="label">Message</label>
          <textarea name="message" v-model="form.message"></textarea>
        </div>
        <button class="button" @click.prevent="submit">Submit form</button>
      </form>
    </div>
  </Layout>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ContactPage',
  metaInfo: {
    title: 'Portfolio'
  },
  data() {
    return {
      form: {
        name: '',
        email: '',
        message: ''
      }
    }
  },
  methods: {
    async submit() {
      try {
        axios({
          method: 'POST',
          url: 'http://106.75.141.156:1337/contacts',
          data: this.form
        })
        window.alert('发送成功')
      } catch (e) {
        window.alert('发送失败，请稍后重试')
      }
    }
  }
}
</script>

<style scoped>
.contact-header {
  padding: 2rem 0 4rem;
}
.contact-title {
  font-size: 4rem;
  margin: 0 0 4rem;
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

input:focus, textarea:focus {
  border-color: var(--color-contrast-1);
}

input, textarea {
  background: transparent;
  border: 1px solid var(--color-base-1);
  outline: none;
  border-radius: .3rem;
  padding: .8rem 1rem;
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
  font-size: .8rem;
  padding: .8rem 1.6rem;
  border-radius: .3rem;
  margin-top: 2rem;
  cursor: pointer;
  transition: opacity .25s ease;
  font-size: 500;
  letter-spacing: .035em;
}

.button:hover {
  opacity: .6;
}

.button:focus {
  border: 1px solid var(--color-base-1);
}
</style>
