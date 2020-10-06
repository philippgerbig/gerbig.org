<template>
  <div v-editable="blok" class="teaser" v-bind:class="classes">
    <img :src="blok.image.filename" class="teaser__image" />
    <div class="teaser__headline-container">
      <h3 class="teaser__headline">
        <span>{{ blok.headline }}</span>
      </h3>
    </div>
    <div class="teaser__content" v-if="blok.description || blok.link">
      <p class="teaser__text">{{ blok.description }}</p>
      <NuxtLink
        :to="blok.link.story.full_slug"
        class="teaser__button"
        v-if="blok.link.story"
        >{{ blok.buttonText || "Mehr zum Thema" }}</NuxtLink
      >
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
  computed: {
    classes: function () {
      return {
        "teaser--image-left": this.blok.imagePosition === "left",
        "teaser--image-right": this.blok.imagePosition === "right",
      };
    },
  },
};
</script>

<style scoped>
.teaser {
  display: grid;
  grid-template-columns: repeat(8, 120px);
  grid-template-rows: repeat(5, 120px);
  margin: 60px auto;
}
.teaser__image {
  grid-area: 1 / 1 / span 3 / span 5;
  z-index: 1;
  position: relative;
}
.teaser__headline-container {
  grid-area: 1 / 5 / span 3 / span 4;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  z-index: 2;
  position: relative;
}
.teaser__headline {
  font-size: 49px;
  line-height: 56px;
  font-weight: bold;
  white-space: pre-wrap;
}
.teaser__headline span {
  display: inline;
  -webkit-box-decoration-break: clone;
  -ms-box-decoration-break: clone;
  -o-box-decoration-break: clone;
  box-decoration-break: clone;
  display: inline;
  background: white;
  box-shadow: 10px 0 0 white, -10px 0 0 white;
  white-space: pre-line;
}
.teaser__text {
font-family: Georgia, "Times New Roman", Times, serif;
}
.teaser__content {
  grid-area: 4 / 4 / span 2 / span 4;
  padding-top: 20px;
  font-size: 20px;
  line-height: 32px;
}

.teaser--image-right .teaser__image {
  grid-area: 1 / 2 / span 3 / span 5;
}
.teaser--image-right .teaser__headline-container {
  grid-area: 1 / 1 / span 3 / span 4;
}
.teaser__button {
  text-transform: uppercase;
  font-weight: bold;
  font-size: 16px;
  padding: 15px 20px;
  line-height: 16px;
  display: inline-block;
  margin-top: 16px;
  background-color: #62B390;
}
</style>
