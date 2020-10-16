<template>
  <div v-editable="blok" class="missing-component">
    <p>Component "{{ blok.component }}" not found!</p>
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
.missing-component {
  padding: 40px;
  text-align: center;
  background: #e74c3c;
  color: #fff;
  font-weight: bold;
}
</style>
