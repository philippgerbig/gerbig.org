<template>
  <component
    v-if="story.content.component"
    :key="story.content._uid"
    :blok="story.content"
    :is="story.content.component"
  />
</template>

<script>
export default {
  props: ['story'],
};
</script>
