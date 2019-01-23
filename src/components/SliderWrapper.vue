<template>
  <div>
    <ul class="wrapper">
      <app-slider-item
        :slider="sliderItems[currentSliderIndex]"
        :moveTo="moveTo"
        @swipe="slideChange"
      ></app-slider-item>
    </ul>

    <app-slider-control
      v-if="sliderItems.length - 1 > currentSliderIndex"
      control="right"
      @slideChange="slideChange"
    ></app-slider-control>
    <app-slider-control
      v-if="currentSliderIndex > 0"
      control="left"
      @slideChange="slideChange"
    ></app-slider-control>

    <app-slider-selectors-wrapper
      :activeSlide="currentSliderIndex"
      :count="sliderItems.length"
      @slideSelected="currentSliderIndex = $event"
    ></app-slider-selectors-wrapper>
  </div>
</template>

<script>
import SliderItem from './SliderItem';
import SliderControl from './SliderControl';
import SliderSelectorsWrapper from './SliderSelectorsWrapper';

import image1 from '../assets/img/1.jpg';
import image2 from '../assets/img/2.jpg';
import image3 from '../assets/img/3.jpg';

export default {
  components: {
    appSliderItem: SliderItem,
    appSliderControl: SliderControl,
    appSliderSelectorsWrapper: SliderSelectorsWrapper
  },

  data() {
    return {
      sliderItems: [
        {
          image: image1,
          heading: 'Heading 1',
          content: 'Content 1'
        },
        {
          image: image2,
          heading: 'Heading 2',
          content: 'Content 2'
        },
        {
          image: image3,
          heading: 'Heading 3',
          content: 'Content 3'
        }
      ],
      moveTo: 'left',
      currentSliderIndex: 0,
      lowerBoundary: 0,
    };
  },

  computed: {
    upperBoundary() {
      return this.sliderItems.length - 1;
    },
    exeededBoundaries() {
      return (
        this.currentSliderIndex < this.lowerBoundary ||
        this.currentSliderIndex > this.upperBoundary
      );
    },
  },

  methods: {
    resetCurrentSliderIndex() {
      this.currentSliderIndex = 0;
    },
    slideChange(direction) {
      this.moveTo = direction;
      if (this.exeededBoundaries) this.resetCurrentSliderIndex();

      if (direction === 'right' && this.currentSliderIndex < this.upperBoundary)
        this.currentSliderIndex++;
      if (direction === 'left' && this.currentSliderIndex > this.lowerBoundary)
        this.currentSliderIndex--;
    }
  }
};
</script>

<style scoped>
.wrapper {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  list-style-type: none;
}
</style>
