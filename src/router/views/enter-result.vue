<script>
import Layout from '@layouts/main.vue'

export default {
  page: {
    title: 'enter result',
    meta: [{ name: 'description', content: 'Enter Test Result' }],
  },
  components: { Layout },
  data() {
    return {
      code: '',
      input: '',
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
    <b-button type="is-primary" class="mb-3" expanded>Submit</b-button>
  </Layout>
</template>
