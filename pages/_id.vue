<template>
  <h1>REDIRECTING...</h1>
</template>

<script>
const COOKIE_NAME = '__shortly__nuxt__'

export default {
  async asyncData({ params, $cookies, redirect }) {
    const { link } = await $cookies.get(`${COOKIE_NAME}${params.id}`)
    redirect(link)
  },
}
</script>
