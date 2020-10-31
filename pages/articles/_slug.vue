<template>
  <div>
    <h1>{{ doc.title }}</h1>
    <nuxt-content :document="doc" />
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const slug = params.slug
    const doc = await $content(slug || 'index').fetch()
    console.log(doc)
    return { slug, doc }
  },
}
</script>