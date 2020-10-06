<template>
  <header class="header" v-editable="blok" v-if="blok">
    <!-- Logo -->
    <nuxt-link to="/" v-if="blok.content.logo">
      <img :src="blok.content.logo.filename" :alt="blok.content.logo.alt" />
    </nuxt-link>

    <!-- Navigation -->
    <nav v-if="blok.content.header_links">
      <ul>
        <li v-for="link in blok.content.header_links" v-bind:key="link.id">
          <nuxt-link :to="link.target.story ? link.target.story.full_slug : link.target.cached_url" v-if="link.target && link.target.linktype === 'story'">
            {{ link.text }}
          </nuxt-link>
          <a :href="link.target.url" v-if="link.target && link.target.linktype === 'url'">{{link.text}}</a>
        </li>
      </ul>
    </nav>
  </header>
</template>


<script>
export default {
  props: ["blok"],
  components: {},
};
</script>

<style>
.header {
  height: 120px;
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-width: 1240px;
  margin: 0 auto;
  align-items: center;
  padding: 0 20px;
}
.header nav ul {
  display: flex;
}
.header nav ul li {
  margin-left: 30px;
  font-size: 12px;
  font-weight: bold;
  text-transform: uppercase;
}
</style>
