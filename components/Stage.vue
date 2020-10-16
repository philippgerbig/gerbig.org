<template>
  <div
    v-editable="blok"
    class="stage"
    :style="{ backgroundColor: blok.backgroundColor ? blok.backgroundColor.color: null }"
    :class="{ 'stage--auto': blok.size === 'auto' }"
  >
    <div class="stage__image" v-if="blok.image && blok.image.filename !== ''">
      <img :src="blok.image ? blok.image.filename : ''" />
    </div>
    <div
      class="stage__text"
      :class="{ 'stage__text--with-shadow': blok.textShadow }"
      :style="{ color: blok.textColor ? blok.textColor.color: null }"
    >
      <h1>{{ blok.headline }}</h1>
      <p v-if="blok.intro">
        {{ blok.intro }}
      </p>
    </div>
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
.stage {
  position: relative;
  height: 600px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.stage--auto {
  height: auto;
  padding: 40px 0;
}

.stage__image {
  position: absolute;
  z-index: 1;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  line-height: 0;
}

.stage__image img {
  height: 100%;
  width: 100%;
  object-fit: cover;
}

.stage__text {
  z-index: 2;
  position: relative;
  color: #fff;
  max-width: 1000px;
  width: 100%;
  padding: 20px;
}
.stage__text--with-shadow {
  text-shadow: 0 0 20px rgba(0, 0, 0, 0.8);
}

h1 {
  font-size: 48px;
  font-weight: bold;
  margin-bottom: 10px;
}
p {
  font-size: 20px;
  line-height: 32px;
  max-width: 360px;
  font-family: Georgia, "Times New Roman", Times, serif;
  font-weight: bold;
}
</style>
