<template>
  <div>
      <p v-if="attempting">Twitterでログインしています。{{success}}</p>
      <template v-else>
        <p>{{failedMessage}}</p>
      </template>
  </div>
</template>

<script>
// import axios from 'axios'

export default {
  data () {
    return {
      failedMessage: null,
      success: null
    }
  },
  async mounted () {
    try {
      // const callbackData = await axios.get(process.env.baseUrl + '/api/login/callback' + '?nocache=' + new Date().getTime(), {
      //   headers: { 'Cache-Control': 'no-cache', 'Pragma': 'no-cache', 'Expires': 0 },
      //   xsrfHeaderName: 'X-CSRF-Token',
      //   params: this.$route.query,
      //   withCredentials: true
      // })
      const callbackData = await this.$axios.get('/api/login/callback', { params: this.$route.query })
      // this.$store.commit('setToken', { token: callbackData.data.access_token })
      // this.$store.commit('setUser', { user: callbackData.data.me })
      console.log(callbackData)
      this.success="成功!!"
      // this.$router.replace('/')
    } catch (error) {
      console.log(error)
      this.failedMessage = error.message
    }
  },
  computed: {
    attempting () {
      return !this.failedMessage
    }
  },
  // methods: {
  // }
}
</script>