<template>
  <div id="single-article">
    <Hero :pageTitle="article.title" :heroImage="article.image" />
    <nuxt-content :document="article" />
  </div>
</template>

<script>
import Hero from '@/components/Hero'
export default {
  components: {
    Hero,
  },
  async asyncData({ $content, params }) {
    const article = await $content(params.slug || 'index').fetch()
    return { article }
  },
}
</script>

<style lang="sass" scoped>
$breakpoint-tablet: 768px

#single-article
  padding: 5% 15%
</style>