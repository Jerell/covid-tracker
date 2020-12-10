<template>
  <section>
    <b-field>
      <b-input
        v-model="name"
        :value="name"
        placeholder="Name"
        @input="persistName"
      ></b-input>
    </b-field>

    <b-field>
      <b-input
        v-model="postcode"
        :value="postcode"
        placeholder="Postcode district"
        pattern="[A-Z]{1,2}\d[A-Z\d]?"
        validation-message="Enter the first half of your postcode."
        @input="update"
      ></b-input>
    </b-field>
    <b-button
      type="is-primary"
      class="mb-3"
      expanded
      @click.native="$emit('done')"
      >Done</b-button
    >

    <p class="my-5">Privacy policy</p>
  </section>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      postcode: '',
    }
  },
  mounted() {
    if (localStorage.name) {
      this.name = localStorage.getItem('name')
      this.postcode = localStorage.getItem('postcode')
    }
  },
  methods: {
    persistName() {
      localStorage.setItem('name', this.name)
    },
    persistPostcode() {
      localStorage.setItem('postcode', this.postcode)
    },
    update() {
      const pattern = RegExp('[A-Z]{1,2}\\d[A-Z\\d]?')
      const valid = pattern.test(this.postcode)
      if (valid) {
        this.persistPostcode()
      }
    },
  },
}
</script>

<style lang="scss" module>
@import '@design';
</style>
