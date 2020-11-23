<script>
import Layout from '@layouts/main.vue'

export default {
  page: {
    title: 'Map',
    meta: [{ name: 'description', content: 'The Map page.' }],
  },
  components: { Layout },
}
</script>

<template>
  <Layout>
    <h1 class="title">Map</h1>
    <p>
      This is gonna show restrictions by region across the UK.
    </p>
  </Layout>
</template>
