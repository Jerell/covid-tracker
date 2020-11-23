<template>
  <section class="pt-1">
    <b-message>
      <p>
        <span class="has-text-weight-bold">
          A high temperature
        </span>
        – this means you feel hot to touch on your chest or back (you do not
        need to measure your temperature)
      </p>
    </b-message>
    <b-message>
      <p>
        <span class="has-text-weight-bold">
          A new, continuous cough
        </span>
        – this means coughing a lot for more than an hour, or 3 or more coughing
        episodes in 24 hours (if you usually have a cough, it may be worse than
        usual)
      </p>
    </b-message>
    <b-message>
      <p>
        <span class="has-text-weight-bold">
          A loss or change to your sense of smell or taste
        </span>
        – this means you've noticed you cannot smell or taste anything, or
        things smell or taste different to normal
      </p>
    </b-message>
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
}
</script>

<style lang="scss" module>
@import '@design';
</style>
