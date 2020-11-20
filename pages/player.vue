<template>
  <section class="container">
    <div>
      <h1>Player</h1>
      <h2>Now playing</h2>
      <iframe
        width="740"
        height="215"
        :src="chobit_links[getRandomInt(chobit_links.length)].chobit_link"
        frameborder="0"
        allowfullscreen
      ></iframe>
      <h2>Track list</h2>
      <b-list-group>
        <b-list-group-item v-for="link in chobit_links" :key="link.id">
          {{ link.id }}
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
      playing: true,
    }
  },
  methods: {
    getRandomInt(max) {
      // ランダムな配列
      return Math.floor(Math.random() * Math.floor(max))
    },
  },
  async asyncData({ app }) {
    const baseUrl = 'https://dojinvoice-api.herokuapp.com/'
    const endPoint = 'v1/chobit'
    const response = await app.$axios.$get(baseUrl + endPoint)
    return { chobit_links: response.data.data }
  },
}
</script>

<style scoped></style>
