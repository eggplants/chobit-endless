<template>
  <section class="container">
    <div>
      <h1>Player</h1>
      <h2>Now playing</h2>
      <iframe
        width="740"
        height="215"
        :src="chobit_links[getRandomInt(chobit_links.length)].chobit_link"
        @load="playerLoaded"
        frameborder="0"
        allowfullscreen
      ></iframe>
      <h2>Track list</h2>
      <b-table
        sticky-header
        :items="chobit_links"
        head-variant="light"
      ></b-table>
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
    const baseUrl = 'https://dojinvoice-api.herokuapp.com'
    const chobitEndPoint = `/v1/chobit?index=${Math.floor(
      Math.random() * Math.floor(20)
    )}&offset=20`
    const chobitLinks = await app.$axios.$get(baseUrl + chobitEndPoint)
    const chobitLinksResponse = chobitLinks.data.data
    const idConvEndPoint = '/v1/ids_to_data?ids='
    var idlist = []
    for (var i = 0; i < chobitLinksResponse.length; i++) {
      idlist.push(chobitLinksResponse[i].id)
    }
    const detailData = await app.$axios.$get(
      baseUrl + idConvEndPoint + idlist.join(',')
    )
    return { chobit_links: chobitLinksResponse, detail_data: detailData }
  },
}
</script>

<style scoped></style>
