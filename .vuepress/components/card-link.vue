<template>
  <a v-if="externalLink" :href="getUrl" target="_blank" rel="noopener noreferrer">
    <main>
      <h4>{{ getTitle }}</h4>
      <p>{{ getDescription }}</p>
    </main>
    <img :src="getImg">
  </a>
  <router-link v-else :to="{ path: getUrl }">
    <main>
      <h4>{{ getTitle }}</h4>
      <p>{{ getDescription }}</p>
    </main>
    <img :src="getImg">
  </router-link>
</template>

<script>
export default {
  props: {
    url: {
      type: String,
      required: true,
    },
    title: {
      type: String
    },
    description: {
      type: String
    },
    img: {
      type: String
    }
  },
  computed: {
    externalLink () {
      return this.getUrl.startsWith("http")
    },
    getTitle () {
      return this.title || this.$page.title || this.$page.frontmatter.title || ""
    },
    getDescription () {
      return this.description || this.$page.description || this.$page.frontmatter.description || ""
    },
    getUrl () {
      return this.url || this.$page.url || this.$page.frontmatter.url || ""
    },
    getImg () {
      return this.img || "https://avatars3.githubusercontent.com/u/34158802?s=400&v=4"
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../styles/palette.styl';
a {
  border: solid 1px $borderColor;
  display: flex;
  justify-content: space-between;
  height: 150px;
  color: $textColor;
  box-shadow: 0 0 4px 0 $borderColor;
}
a:hover {
  border-color: $accentColor;
  text-decoration: none!important;
  box-shadow: 0 0 10px 0 $borderColor;
}
a:hover h4 {
  color: $accentColor;
}
main {
  padding: 1em;
}
h4 {
  margin-top: 0;
}
p {
  color: lighten($textColor, 40);
  font-size: .9em;
}
img {
  height: 150px;
  width: 150px;
}
@media (max-width: $MQMobileNarrow) {
  p {
    display: none;
  }
}
</style>
