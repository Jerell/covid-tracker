<script>
/* eslint-disable eqeqeq */
export default {
  props: {
    pend: { type: Number, default: 0 },
  },
  data() {
    return {
      end: this.pend ? this.pend : 0,
      remaining: '',
    }
  },
  mounted() {
    if (localStorage.name) {
      this.end = localStorage.getItem('isolation-end')
    }
    this.secondsToDhms()
  },
  methods: {
    setTime() {
      const days = 10
      const now = new Date()
      console.log(now)
      this.end = new Date(now).setDate(now.getDate() + days)
      this.persistTime()
      this.secondsToDhms()
    },
    persistTime() {
      localStorage.setItem('isolation-end', this.end)
    },
    secondsToDhms() {
      if (new Date(this.end) < new Date()) {
        this.end = 0
        localStorage.removeItem('isolation-end')
      }
      if (!this.end) {
        return
      }
      const seconds = Math.floor((this.end - new Date()) / 1000)
      const d = Math.floor(seconds / (3600 * 24))
      const h = Math.floor((seconds % (3600 * 24)) / 3600)
      const m = Math.floor((seconds % 3600) / 60)
      const s = Math.floor(seconds % 60)

      const dDisplay = d > 0 ? d + (d == 1 ? ' day, ' : ' days, ') : ''
      const hDisplay = h > 0 ? h + (h == 1 ? ' hour, ' : ' hours, ') : ''
      const mDisplay = m > 0 ? m + (m == 1 ? ' minute, ' : ' minutes, ') : ''
      const sDisplay = s > 0 ? s + (s == 1 ? ' second' : ' seconds') : ''
      this.remaining = dDisplay + hDisplay + mDisplay + sDisplay
      if (this.end >= 1) {
        setTimeout(() => {
          this.secondsToDhms()
        }, 1000)
      }
    },
  },
}
</script>

<template>
  <section>
    <h5 class="title has-text-white is-5 m-0">You should self-isolate for</h5>
    <h3 class="title has-text-white is-3 mb-2">{{ remaining }}</h3>
  </section>
</template>

<style lang="scss" module>
@import '@design';
</style>
