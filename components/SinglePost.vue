<template>
  <div id="post" v-editable="editable">
    <Hero :hero-image="image" :page-title="title" class="post-thumbnail" />
    <main>
      <no-ssr>
        <!-- eslint-disable-next-line -->
        <article class="post-detail" v-html="blogContent"></article>
      </no-ssr>
    </main>
    <Author name="Kofi Obrasi Ocran" image="/ocran.jpeg" />
  </div>
</template>

<script>
import Author from '@/components/Blog/Author'
import Hero from '@/components/Hero/Hero'
export default {
  components: {
    Author,
    Hero,
  },
  props: {
    image: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    content: {
      type: Object,
      required: true,
    },
    editable: {
      type: Object,
      required: true,
    },
  },
  computed: {
    blogContent() {
      return this.$storyapi.richTextResolver.render(this.content)
    },
  },
}
</script>

<style scoped>
#post {
  margin: 0 0 1rem;
}
main {
  margin: 3rem 20% 6rem;
}
article {
  flex-grow: 1;
}
.post-thumbnail {
  height: 300px;
}
.post-detail {
  margin: 0 auto 10em;
}
@media (max-width: 768px) {
  main {
    margin: 3rem 5%;
  }
}
</style>
