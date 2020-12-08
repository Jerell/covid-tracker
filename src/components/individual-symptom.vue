<script>
export default {
  props: {
    lead: { type: String, default: 'symptom' },
    desc: { type: String, default: 'description' },
    affected: { type: Boolean, default: false },
    n: { type: Number, default: 0 },
  },
  computed: {
    style() {
      return this.affected ? { boxShadow: '0 0 15px green inset' } : {}
    },
    type() {
      return this.affected ? 'is-danger' : ''
    },
  },
}
</script>

<template>
  <b-message :type="type" @click.native="$emit('toggle', n)">
    <p>
      <span class="has-text-weight-bold">
        {{ lead }}
      </span>
      – {{ desc }}
    </p>
  </b-message>
</template>

<style lang="scss" module>
@import '@design';
</style>
