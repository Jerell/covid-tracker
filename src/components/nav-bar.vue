<script>
import { authComputed } from '@state/helpers'
import NavBarRoutes from './nav-bar-routes.vue'

export default {
  components: { NavBarRoutes },
  data() {
    return {
      persistentNavRoutes: [
        {
          name: 'home',
          title: 'Advice',
          icon: 'book-open-variant',
        },
        {
          name: 'map',
          title: 'Map',
          icon: 'map',
        },
        {
          name: 'symptoms',
          title: 'Symptom Checker',
          icon: 'thermometer-alert',
        },
        {
          name: 'result',
          title: 'Enter test result',
          icon: 'test-tube',
        },
      ],
      loggedInNavRoutes: [
        {
          name: 'profile',
          title: () => 'Logged in as ' + this.currentUser.name,
          icon: 'book-open-variant',
        },
        {
          name: 'logout',
          title: 'Log out',
          icon: 'book-open-variant',
        },
      ],
      loggedOutNavRoutes: [
        {
          name: 'login',
          title: 'Log in',
          icon: 'book-open-variant',
        },
      ],
    }
  },
  computed: {
    ...authComputed,
  },
}
</script>

<template>
  <div class="is-ancestor">
    <ul :class="$style.container">
      <NavBarRoutes :routes="persistentNavRoutes" />
      <NavBarRoutes v-if="loggedIn" :routes="loggedInNavRoutes" />
      <!-- <NavBarRoutes v-else :routes="loggedOutNavRoutes" /> -->
    </ul>
  </div>
</template>

<style lang="scss" module>
@import '@design';

.container {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0;
  margin: 0 0 $size-grid-padding;
  text-align: center;
  list-style-type: none;

  > li {
    display: block;
    margin-right: $size-grid-padding;
    text-align: left;
  }
}
</style>
