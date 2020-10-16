<template>
  <div v-editable="blok" class="page">
    <Header
      v-if="blok.header"
      :blok="blok.header"
      v-editable="blok.header"
      :key="blok.header._uid"
    />
    <div class="body">
      <component
        v-for="blok in blok.body"
        :key="blok._uid"
        :blok="blok"
        :is="blok.component"
      />
    </div>

    <Footer
      v-if="blok.footer"
      :blok="blok.footer"
      v-editable="blok.footer"
      :key="blok.footer._uid"
    />
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
.page {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.body {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}
</style>
