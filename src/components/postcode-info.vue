<script>
import PostcodeMap from '@components/postcode-map.vue'
const fetch = require('node-fetch')

export default {
  components: {
    PostcodeMap,
  },
  data() {
    return {
      postcode: '',
      tier: 0,
      restrictions: [
        ['None'],
        [
          'Follow the rule of six if meeting indoors or outdoors',
          'Pubs and restaurants to shut at 11pm',
          'People encouraged to minimise travel and work from home where possible',
          'Spectators allowed at sports events and live performances (limited numbers)',
          'Personal care including hairdressing allowed',
        ],
        [
          'No household mixing indoors',
          'Rule of six will apply outdoors',
          'Pubs and restaurants to shut at 11pm',
          'Alcohol only served as part of substantial meal',
          'Spectators allowed at sports events and live performances (limited numbers)',
          'Personal care including hairdressing allowed',
        ],
        [
          'No household mixing indoors or outdoors in hospitality venues or private gardens',
          'Rule of six applies in outdoor public spaces like parks',
          'Pubs/restaurants closed except for delivery and takeaway',
          'Indoor entertainment venues closed',
          'Guidance against travelling in and out of the area',
          'Personal care including hairdressing allowed',
        ],
      ],
    }
  },
  mounted() {
    if (localStorage.postcode) {
      this.postcode = localStorage.getItem('postcode')
    }
    if (!localStorage.tiers) {
      this.getTiers()
    } else {
      this.tier = JSON.parse(localStorage.tiers)[this.postcode]
    }
  },
  methods: {
    async getTiers() {
      const response = await fetch(
        `http://covid19-middleware.herokuapp.com/api/getAllRestrictions`
      )
      const json = await response.json()
      console.log(json)
      console.log(this.postcode)
      localStorage.setItem('tiers', JSON.stringify(json))
      this.tier = json[this.postcode]
      location.reload()
      // return json
    },
  },
}
</script>

<template>
  <section v-if="postcode.length > 0">
    <div class="status">
      <p>Your postcode district</p>
      <h3 class="title has-text-white is-3 m-0">{{ postcode }}</h3>
      <h4 class="title has-text-white is-4">Restriction tier: {{ tier }}</h4>
    </div>
    <p class="my-2">The restrictions in place are as follows:</p>
    <p v-for="r in restrictions[tier]" :key="r">{{ r }}</p>
    <PostcodeMap></PostcodeMap>
  </section>
</template>

<style lang="scss" module>
@import '@design';
</style>
