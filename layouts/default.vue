<template>
  <Nuxt />
</template>

<script>
import Header from "~/components/Header.vue";
import Footer from "~/components/Footer.vue";
export default {
  components: {
    Header,
    Footer,
  },
  computed: {
    currentPage() {
      console.log("route", this.$route);
      return this.$route.path.length >= 0 ? this.$route.path.substr(1) : "";
    },
  },
};
</script>

<style>
.layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.content {
  flex-grow: 1;
  flex-direction: column;
}

html {
  font-family: Helvetica, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}
</style>
