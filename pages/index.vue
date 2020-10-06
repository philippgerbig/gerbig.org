<template>
  <div class="page">
    <Header :blok="story.content.header" />

    <component
      v-if="story.content.component"
      :key="story.content._uid"
      :blok="story.content"
      :is="story.content.component"
    />

    <Footer :blok="story.content.footer" />
  </div>
</template>

<script>
import Header from "../components/Header";
import PageContent from "../components/PageContent";
export default {
  components: { PageContent },
  data() {
    return {
      story: { content: {} },
    };
  },
  mounted() {
    // Use the input event for instant update of content
    this.$storybridge.on(
      "input",
      (event) => {
        if (event.story.id === this.story.id) {
          event.story.content.header = this.story.content.header
          event.story.content.footer = this.story.content.footer
          this.story = event.story
        }
      }
    );
    // this.$storybridge.resolveRelations(["header"], (data) => {
    //   console.log("data", data);
    // });
    // Use the bridge to listen the events
    this.$storybridge.on(["published", "change"], (event) => {
      // window.location.reload()
      this.$nuxt.$router.go({
        path: this.$nuxt.$router.currentRoute,
        force: true,
      });
    });
  },
  async fetch(context) {
    // Loading reference data - Articles in our case
    if (context.store.state.articles.loaded !== "1") {
      let articlesRefRes = await context.app.$storyapi.get(`cdn/stories/`, {
        starts_with: "articles/",
        version: "draft",
      });
      context.store.commit("articles/setArticles", articlesRefRes.data.stories);
      context.store.commit("articles/setLoaded", "1");
    }
  },
  async asyncData(context) {
    // // This what would we do in real project
    // const version = context.query._storyblok || context.isDev ? 'draft' : 'published'
    // const fullSlug = (context.route.path == '/' || context.route.path == '') ? 'home' : context.route.path

    const options = {
      version: "draft",
      resolve_relations: "header,footer",
      resolve_links: 'url'
    };

    // Load the JSON from the API - loadig the home content (index page)
    const requests = [
      context.app.$storyapi.get("cdn/stories/home", options),
      // context.app.$storyapi.get("cdn/stories/_global/footer", options);
    ];

    return Promise.all(requests)
      .then((responses) => {
        const story = responses[0].data.story;
        return {
          story,
        };
      })
      .catch((errors) => {
        console.error(errors);
      });
  },
};
</script>
<style scoped>
.content {
  display: flex;
  flex-direction: column;
}
</style>
