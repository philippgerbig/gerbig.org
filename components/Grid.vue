<template>
  <div class="grid" v-editable="blok">
    <ul class="container">
      <li :key="blok._uid" v-for="blok in blok.columns" class="flex-auto px-6">
        <component :blok="blok" :is="blok.component" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    blok: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 1200px;
  padding: 0 20px;
  display: flex;
  margin: 120px auto;
}
</style>
