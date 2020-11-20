<template>
  <section class="container">
    <div>
      <b-list-group>
        <b-list-group-item
          v-for="track in tracks.data.v1_endpoints"
          :key="track"
        >
          {{ track }}
        </b-list-group-item>
      </b-list-group>
    </div>
  </section>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      tracks: [],
    }
  },
  methods: {},
  async asyncData({ app }) {
    const baseUrl = 'https://dojinvoice-api.herokuapp.com/'
    const response = await app.$axios.$get(baseUrl)
    return { tracks: response }
  },
}
</script>

<style scoped></style>
