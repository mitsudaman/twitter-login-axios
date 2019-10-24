<template>
  <div>
    <p>Twitterへリダイレクトしています</p>
  </div>
</template>

<script>

export default {
  components: {
  },
  asyncData ({ app,context, error }) {
    return app.$axios.$get('/api/login/twitter')
      .then(data => {
        return { twitterAuthUrl: data.redirect_url }
      })
      .catch(e => error({ message: e.message, statusCode: e.statusCode }))
  },

  mounted () {
    window.location.href = this.twitterAuthUrl
  }
}
</script>