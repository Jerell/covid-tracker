<script>
import Layout from '@layouts/main.vue'
import IsolationTimer from '@/src/components/isolation-timer.vue'

const fetch = require('node-fetch')

export default {
  page: {
    title: 'enter result',
    meta: [{ name: 'description', content: 'Enter Test Result' }],
  },
  components: { Layout, IsolationTimer },
  data() {
    return {
      code: '',
      input: '',
      end: 0,
      loading: false,
    }
  },
  methods: {
    update() {
      const pattern = RegExp('\\w{6}')
      const valid = pattern.test(this.input)
      if (valid) {
        this.code = this.input
      } else {
        this.code = ''
      }
    },
    async check() {
      if (!this.code.length) {
        return
      }
      this.loading = true
      try {
        const response = await fetch(
          `http://covid19-middleware.herokuapp.com/api/verifyPositiveTest/${this.code}`
        )
        const json = await response.json()
        console.log(json)
      } catch {
        console.log('Fetch failed')
      }
      this.loading = false
      this.setTime()
    },
    persistTime() {
      localStorage.setItem('isolation-end', this.end)
    },
    setTime() {
      console.log('setting')
      const days = 10
      const now = new Date()
      this.end = new Date(now).setDate(now.getDate() + days)
      this.persistTime()
    },
  },
}
</script>

<template>
  <Layout>
    <h1 class="title has-text-white mb-0">Enter Test Result</h1>
    <b-field label="Confirmation code">
      <b-input
        v-model="input"
        size="is-large"
        expanded
        placeholder="ABCXYZ"
        pattern="\w{6}"
        validation-message="Enter your six character confirmation code"
        maxlength="6"
        @input="update"
      ></b-input>
    </b-field>
    <b-button
      type="is-primary"
      class="mb-3"
      expanded
      :loading="loading"
      @click="check"
      >Submit</b-button
    >
    <IsolationTimer v-if="end" :end="end"></IsolationTimer>
  </Layout>
</template>
