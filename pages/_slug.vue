<template>
    <component
      v-if="story.content.component"
      :is="story.content.component"
      :blok="story.content"
      :key="story.content._uid"
    />
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
  head() {
    return {
      htmlAttrs: { lang: "de" },
    };
  },
  mounted() {
    // Use the input event for instant update of content
    this.$storybridge.on("input", (event) => {
      if (event.story.id === this.story.id) {
        event.story.content.header = this.story.content.header;
        event.story.content.footer = this.story.content.footer;
        this.story = event.story;
      }
    });
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
  async asyncData(context) {
    const options = {
      version: "draft",
      resolve_relations: "header,footer",
      resolve_links: "url",
    };

    const response = await context.app.$storyapi.get(
      `cdn/stories${context.route.path}`,
      options
    );
    return { story: response.data.story };
  },
};
</script>
