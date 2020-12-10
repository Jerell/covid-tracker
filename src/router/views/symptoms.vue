<script>
import Layout from '@layouts/main.vue'
import SymptomChecker from '@components/symptom-checker.vue'

export default {
  page: {
    title: 'Symptoms',
    meta: [{ name: 'description', content: 'The Symptoms page.' }],
  },
  components: { Layout, SymptomChecker },
  methods: {
    redirect() {
      location.replace('/enter-result')
    },
  },
}
</script>

<template>
  <Layout>
    <h1 class="title has-text-white">Symptom Checker</h1>
    <SymptomChecker></SymptomChecker>

    <b-button
      type="is-link is-light"
      class="my-3"
      expanded
      @click.native="redirect"
      >Enter test results</b-button
    >
  </Layout>
</template>
