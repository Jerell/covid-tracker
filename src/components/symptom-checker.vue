<template>
  <section class="pt-1">
    <individualsymptom
      v-for="(symptom, i) in symptoms"
      :key="i"
      v-bind="symptom"
      :n="i"
      @toggle="toggleAffected"
    ></individualsymptom>
    <b-button type="is-link" class="my-3" expanded :disabled="!canBook"
      >Book a test</b-button
    >
  </section>
</template>

<script>
import individualsymptom from '@components/individual-symptom.vue'
export default {
  components: { individualsymptom },
  data() {
    return {
      symptoms: [
        {
          lead: 'A high temperature',
          desc:
            'this means you feel hot to touch on your chest or back (you do not need to measure your temperature)',
          affected: false,
        },
        {
          lead: 'A new, continuous cough',
          desc:
            'this means coughing a lot for more than an hour, or 3 or more coughing episodes in 24 hours (if you usually have a cough, it may be worse than usual)',
          affected: false,
        },
        {
          lead: 'A loss or change to your send of smell or taste',
          desc:
            "this means you've noticed you cannot smell or taste anything, or things smell or taste different to normal",
          affected: false,
        },
      ],
      canBook: false,
    }
  },
  methods: {
    toggleAffected(n) {
      this.symptoms[n].affected = !this.symptoms[n].affected
      this.check()
    },
    check() {
      if (this.symptoms.map((s) => s.affected).every((a) => a)) {
        this.canBook = true
      } else {
        this.canBook = false
      }
    },
  },
}
</script>

<style lang="scss" module>
@import '@design';
</style>
