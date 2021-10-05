<template>
  <div>
    <Navbar></Navbar>
    <Header></Header>
    <Shortener :links="links" @create-link="createLink"></Shortener>
  </div>
</template>

<script>
const COOKIE_NAME = '__shortly__nuxt__'

export default {
  asyncData({ $cookies }) {
    const allCookies = $cookies.getAll()
    const allRedirectCookies = Object.keys(allCookies).filter(
      (key) => key.slice(0, COOKIE_NAME.length) === COOKIE_NAME
    )

    const links = allRedirectCookies.map((cookie) => allCookies[cookie])

    return { links }
  },
  methods: {
    createLink(linkObj) {
      const oneMonth = 60 * 60 * 24 * 31
      this.links.unshift(linkObj)
      this.$cookies.set(
        `${COOKIE_NAME}${linkObj.id}`,
        JSON.stringify(linkObj),
        {
          maxAge: oneMonth,
          sameSite: 'strict',
        }
      )
    },
  },
}
</script>
