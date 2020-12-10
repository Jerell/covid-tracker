<script>
export default {
  data() {
    return {
      postcode: '',
      risk: Math.ceil(Math.random() * Math.floor(4)),
      restrictions: [
        'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        'Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
        'Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.',
        'Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.',
      ],
    }
  },
  mounted() {
    if (localStorage.postcode) {
      this.postcode = localStorage.getItem('postcode')
    }
  },
}
</script>

<template>
  <section v-if="postcode.length > 0">
    <div class="status">
      <p>Your postcode district</p>
      <h3 class="title has-text-white is-3 m-0">{{ postcode }}</h3>
      <h4 class="title has-text-white is-4">Risk level: {{ risk }}</h4>
    </div>
    <p class="my-2">The restrictions in place are as follows:</p>
    <p v-for="r in restrictions.slice(0, risk)" :key="r">{{ r }}</p>
  </section>
</template>

<style lang="scss" module>
@import '@design';
</style>
