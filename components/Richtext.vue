<template>
  <div
    v-editable="blok"
    class="richtext">
    <rich-text-renderer
      :document="blok.body"
    />
  </div>
</template>

<script>
export default {
  props: {
    blok: {
      type: Object,
      required: true
    }
  }
}
</script>
<style scoped>
.richtext {
  max-width: 720px;
  margin: 60px auto;
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-size: 20px;
  line-height: 32px;
}

p {
  margin-bottom: 32px;
}
</style>
