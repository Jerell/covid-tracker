<template>
  <section>
    <b-field>
      <b-input v-model="name" placeholder="Name" @input="persistName"></b-input>
    </b-field>

    <b-field>
      <b-input
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

    <p class="my-5" @click="wipe">Clear all info and reset</p>
  </section>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      postcode: '',
      input: '',
    }
  },
  mounted() {
    if (localStorage.name || localStorage.postcode) {
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
    update(e) {
      this.input = e
      const pattern = RegExp('[A-Z]{1,2}\\d[A-Z\\d]?')
      const valid = pattern.test(this.input)
      if (valid) {
        this.postcode = this.input
      } else {
        this.postcode = ''
      }
      this.persistPostcode()
    },
    wipe() {
      const storedItems = [
        'name',
        'postcode',
        'privacy-agreement-accepted',
        'tiers',
      ]
      for (const item of storedItems) {
        localStorage.removeItem(item)
      }
      location.reload()
    },
  },
}
</script>

<style lang="scss" module>
@import '@design';
</style>
