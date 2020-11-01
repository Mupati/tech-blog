<template>
  <div id="container">
    <ArticlePreview
      v-for="article in articles"
      :key="article.slug"
      :slug="article.slug"
      :title="article.title"
      :excerpt="article.description"
      :image="article.image"
    />
  </div>
</template>

<script>
import ArticlePreview from '@/components/ArticlePreview'
export default {
  components: {
    ArticlePreview,
  },
  async asyncData({ $content, params }) {
    const articles = await $content().fetch()
    return { articles }
  },
}
</script>

<style lang="scss" scoped>
#container {
  padding: 5% 15%;
}
</style>