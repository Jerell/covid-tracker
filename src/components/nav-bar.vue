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
          name: 'symptoms',
          title: 'Symptom Checker',
          icon: 'thermometer-alert',
        },
        {
          name: 'enter-result',
          title: 'Enter test result',
          icon: 'test-tube',
        },
        // {
        //   name: 'map',
        //   title: 'Map',
        //   icon: 'map',
        // },
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
  <section class="nav">
    <div class="is-ancestor">
      <ul :class="$style.container">
        <NavBarRoutes :routes="persistentNavRoutes" />
        <NavBarRoutes v-if="loggedIn" :routes="loggedInNavRoutes" />
        <!-- <NavBarRoutes v-else :routes="loggedOutNavRoutes" /> -->
      </ul>
    </div>
  </section>
</template>

<style lang="scss" module>
@import '@design';

section.nav {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0;
  margin: 0 0 $size-grid-padding;
  text-align: center;
  list-style-type: none;
}
</style>
