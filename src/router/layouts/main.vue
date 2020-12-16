<script>
import NavBar from '@components/nav-bar.vue'
import PrivacyInfo from '@components/privacy-info.vue'

export default {
  components: { NavBar, PrivacyInfo },
  data() {
    return {
      privacyAccepted: localStorage['privacy-agreement-accepted'],
    }
  },
}
</script>

<template>
  <div :class="$style.container">
    <h1 class="title has-text-white p-1">COVID-19 Track & Trace</h1>
    <PrivacyInfo v-if="!privacyAccepted"></PrivacyInfo>
    <div v-else>
      <slot />
      <NavBar class="mt-3 py-3" />
    </div>
  </div>
</template>

<style lang="scss" module>
@import '@design';

.container {
  position: relative;
  box-sizing: border-box;
  min-width: $size-content-width-min;
  max-width: $size-content-width-max;
  min-height: 100%;
  padding: 0 10px;
  margin: 0 auto;
}
</style>
