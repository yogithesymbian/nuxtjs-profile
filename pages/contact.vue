<template>
  <div>
    <nuxt keep-alive />
    <p v-if="$fetchState.pending">Fetching mountains...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-else>
      <h1>Nuxt Mountains</h1>
      <ul>
        <li v-for="mountain of mountains" :key="mountain.title">
          {{ mountain.title }}
        </li>
      </ul>
      <button @click="$fetch">Refresh</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      mountains: [],
      posts: [],
    }
  },
  async fetch() {
    this.mountains = await fetch('https://api.nuxtjs.dev/mountains').then(
      (res) => res.json()
    )
    this.posts = await fetch('https://api.nuxtjs.dev/posts').then((res) =>
      res.json()
    )
  },
  // watch in Network of inspect element
  watch: {
    '$route.query': '$fetch',
  },
  // call fetch only on client-side
  // fetchOnServer: false,
}
</script>
