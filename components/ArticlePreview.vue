<template>
  <nuxt-link :to="`articles/${slug}`" class="post-preview">
    <article>
      <div
        class="post-preview-thumbnail"
        :style="{ backgroundImage: 'url(' + image + ')' }"
      ></div>
      <div class="post-preview-content">
        <h1>{{ title }}</h1>
        <span id="divider"></span>
        <p>{{ excerpt }}</p>
      </div>
    </article>
  </nuxt-link>
</template>

<script>
export default {
  props: {
    slug: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    excerpt: {
      type: String,
      required: true,
    },
    image: {
      type: String,
      required: true,
    },
  },
}
</script>

<style scoped>
a {
  text-decoration: none;
  color: #000;
}
.post-preview {
  box-shadow: 1px 1px 5px 1px rgba(0, 0, 0, 0.2);
  margin: 10px 20%;
}
.post-preview:hover {
  box-shadow: 1px 1px 5px 1px rgba(0, 0, 0, 0.5);
}
article {
  display: flex;
}
.post-preview-thumbnail {
  background-position: center;
  background-size: cover;
  min-width: 15em;
}

.post-preview-content {
  padding: 3em 2em;
}
#divider {
  display: block;
  width: 3rem;
  background-color: #06c4d1;
  height: 2px;
}
@media (max-width: 768px) {
  .post-preview {
    margin: 10px 2%;
  }
}
@media (max-width: 600px) {
  .post-preview {
    margin: 10px 2%;
  }
  article {
    flex-direction: column;
  }
  .post-preview-thumbnail {
    min-height: 15em;
  }
}
</style>
