<script>
export default {
  methods: {
    accept() {
      localStorage.setItem('privacy-agreement-accepted', true)
      location.reload()
    },
  },
}
</script>

<template>
  <section>
    <h2 class="title has-text-white is-2 mb-2">Privacy agreement</h2>
    <p class="pr-2"
      >Holding on to your private information is a serious responsibility, and
      we want you to know how we're handling it.</p
    >
    <h4 class="subtitle has-text-white is-4 my-2"
      >What we record on your device</h4
    >
    <p
      >Your
      <span class="has-text-weight-bold">
        NAME
      </span>
      is used to enhance the UI. It is only visible to you.
    </p>
    <p class="pr-2"
      >Your
      <span class="has-text-weight-bold">
        POSTCODE DISTRICT
      </span>
      (the first bit of your postcode) is used to filter restriction information
      so you see what's most relevant to you.
    </p>
    <p class="pr-2"
      >The
      <span class="has-text-weight-bold">
        ANONYMOUS TOKENS
      </span>
      of the other users you encounter.
    </p>
    <p class="pr-2"
      >The
      <span class="has-text-weight-bold">
        ANONYMOUS TOKENS
      </span>
      of the venues you visit.
    </p>
    <h4 class="subtitle has-text-white is-4 my-2"
      >What we transmit from your device</h4
    >
    <p
      >Your
      <span class="has-text-weight-bold">
        ANONYMOUS TOKEN.
      </span>
      Each day your device will randomly generate an anonymous token shared with
      other users.
    </p>
    <p
      >Your
      <span class="has-text-weight-bold">
        TEST CONFIRMATION CODE
      </span>
      is sent to your healthcare provider when you enter your test result in
      this app. This is simply to verify that you did actually take a test
      before we tell you to self isolate.
    </p>
    <h4 class="subtitle has-text-white is-4 my-2">What we send to you</h4>
    <p
      >The
      <span class="has-text-weight-bold">
        ANONYMOUS TOKENS
      </span>
      of users and venues that test positive for COVID-19. If any of these match
      those recorded on your device, you will be notified.
    </p>
    <b-button type="is-primary my-3" expanded to="/" @click="accept"
      >Accept</b-button
    >
  </section>
</template>

<style lang="scss" module>
@import '@design';
</style>
