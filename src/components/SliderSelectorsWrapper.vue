<template>
  <span class="slider-selectors">
    <app-slider-selector
      :active="activeSlide === index"
      v-for="(selector, index) in count"
      :key="selector"
      @slideSelected="$emit('slideSelected', index)"
    ></app-slider-selector>
  </span>
</template>

<script>
import SliderSelector from "./SliderSelector";

export default {
  props: ['count', 'activeSlide'],

  components: {
    appSliderSelector: SliderSelector
  }
};
</script>

<style scoped>
.slider-selectors {
  display: flex;
  position: absolute;
  bottom: 1%;
  left: 50%;
  transform: translateX(-50%);
}
</style>
