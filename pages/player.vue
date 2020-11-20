<template>
  <section class="container">
    <div>
      <h1>Player</h1>
      <h2>Now playing</h2>
      <h2>Track list</h2>
      {{ response }}
      <!-- <b-list-group>
        <b-list-group-item
          v-for="track in tracks.data.v1_endpoints"
          :key="track"
        >
          {{ track }}
        </b-list-group-item>
      </b-list-group> -->
    </div>
  </section>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      playing: true,
    }
  },
  methods: {},
  async asyncData({ app }) {
    const baseUrl = 'https://dojinvoice-api.herokuapp.com/'
    const response = await app.$axios.$get(baseUrl)
    return { response }
  },
}
</script>

<style scoped></style>
