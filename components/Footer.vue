<template>
  <footer class="footer">
    <!-- Logo Icon -->
    <div class="footer__logo">
      <nuxt-link to="/" title="Startseite">
        <img
          :src="blok.content.icon.filename"
          :alt="blok.content.icon.alt"
          v-if="blok.content.icon"
        />
      </nuxt-link>
    </div>

    <!-- Social Links -->
    <div v-if="blok.content.social_links" class="footer__social-links">
      <ul>
        <li v-for="link in blok.content.social_links" v-bind:key="link.id">
          <a :href="link.url.url" target="_blank" :title="link.title">
            <img :src="link.icon.filename" :alt="link.icon.alt" />
          </a>
        </li>
      </ul>
    </div>

    <!-- Navigation -->
    <nav v-if="blok.content.footer_links" class="footer__links">
      <ul>
        <li v-for="link in blok.content.footer_links" v-bind:key="link.id">
          <nuxt-link :to="link.target.story ? link.target.story.url : link.target.cached_url" v-if="link.target.linktype === 'story'"> {{ link.text }} </nuxt-link>
        </li>
      </ul>
    </nav>
  </footer>
</template>


<script>
export default {
  props: ["blok"],
  components: {},
};
</script>

<style scoped>
.footer {
  display: flex;
  width: 100%;
  max-width: 1240px;
  margin: 0 auto;
  align-items: center;
  padding: 40px 20px;
}

.footer__social-links,
.footer__links,
.footer__logo {
  flex-grow: 0;
  max-width: 33.333333%;
  flex-basis: 33.333333%;
}
.footer__social-links ul,
.footer__links ul {
  display: flex;
  justify-content: flex-end;
}
.footer__links a {
  text-transform: uppercase;
  margin-left: 20px;
  color: #888;
  font-size: 12px;
  font-weight: bold;
}

.footer__social-links a {
  padding: 8px;
  display: block;
}
.footer__social-links img {
  width: 32px;
}
</style>
