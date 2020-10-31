<template>
  <header id="hero" :style="{ backgroundImage: 'url(' + heroImage + ')' }">
    <h1>{{ pageTitle }}</h1>
  </header>
</template>

<script>
export default {
  props: {
    heroImage: {
      type: String,
      required: true,
    },
    pageTitle: {
      type: String,
      default: '',
    },
  },
}
</script>

<style scoped>
#hero {
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 60vh;
}
header {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}
header::before {
  content: '';
  display: block;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #000;
  opacity: 0.65;
}
h1 {
  text-align: center;
  z-index: 2;
  color: #06c4d1;
  font-size: 5em;
}
@media (max-width: 768px) {
  h1 {
    font-size: 2.5em;
  }
}
</style>
