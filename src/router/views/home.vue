<script>
// import Vue from 'vue'
import appConfig from '@src/app.config'
import Layout from '@layouts/main.vue'
import RegistrationForm from '@components/registration-form.vue'
import PostcodeInfo from '@components/postcode-info.vue'
import IsolationTimer from '@components/isolation-timer.vue'

export default {
  components: { Layout, RegistrationForm, PostcodeInfo, IsolationTimer },
  data() {
    return {
      name: '',
      postcode: '',
      message: localStorage.name
        ? `Welcome, ${localStorage.name}`
        : "Let's get started",
      editing: false,
    }
  },
  page: {
    title: 'Home',
    meta: [{ name: 'description', content: appConfig.description }],
  },
  mounted() {
    if (localStorage.name) {
      this.name = localStorage.getItem('name')
      this.postcode = localStorage.getItem('postcode')
    }
  },
  methods: {
    toggleEditMode() {
      if (this.editing) {
        location.reload()
      }
      this.editing = !this.editing
    },
  },
}
</script>

<template>
  <Layout>
    <h1 class="subtitle is-3 has-text-white"
      >{{ message }}
      <b-button
        :class="{ 'is-primary is-light': editing }"
        @click="toggleEditMode"
        ><b-icon icon="pencil"></b-icon></b-button
    ></h1>
    <RegistrationForm v-if="editing" @done="toggleEditMode"></RegistrationForm>
    <IsolationTimer></IsolationTimer>
    <PostcodeInfo></PostcodeInfo>
  </Layout>
</template>

<style lang="scss" module>
@import '@design';
</style>
