<template>
  <h1>REDIRECTING...</h1>
</template>

<script>
const COOKIE_NAME = '__shortly__nuxt__'

export default {
  beforeMount() {
    const { id } = this.$route.params
    const link = this.$cookies.get(`${COOKIE_NAME}${id}`)

    window.location = link.link
  },
}
</script>
