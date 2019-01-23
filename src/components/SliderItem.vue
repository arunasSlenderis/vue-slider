<template>
  <transition
    :name="moveTo === 'left' ? 'slide-left' : 'slide-right'"
  >
    <li
      class="slider-item"
      :style="background"
      :key="slider.heading"
    >
      <div class="slider-item-wrapper">
        <h1 class="slider-item-heading">{{ slider.heading }}</h1>
        <p class="slider-item-text">{{ slider.content }}</p>
      </div>
    </li>
  </transition>
</template>

<script>
export default {
  props: ['slider', 'moveTo'],

  data() {
    return {
      startCoord: 0,
      endCoord: 0
    }
  },

  computed: {
    background() {
      return { 'background-image': `url('${this.slider.image}')` };
    }
  },

  mounted() {
    const vm = this;

    document.addEventListener('touchstart', vm.onTouchStart);
    document.addEventListener('touchend', vm.onTouchEnd);
  },

  destroyed() {
    document.removeEventListener('touchstart', vm.onTouchStart);
    document.removeEventListener('touchend', vm.onTouchEnd);
  },

  methods: {
    _pickCoordinates(e) {
      return e.changedTouches[0].clientX
    },
    _emitSwipeDirection() {
      if (this.endCoord < this.startCoord) this.$emit('swipe', 'right');
      if (this.endCoord > this.startCoord) this.$emit('swipe', 'left');
    },
    onTouchStart(e) {
      this.startCoord = this._pickCoordinates(e);
    },
    onTouchEnd(e) {
      this.endCoord = this._pickCoordinates(e);
      this._emitSwipeDirection();
    }
  }
};
</script>

<style scoped>
.slider-item {
  width: 100vw;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.slider-item-wrapper {
  font-family: 'Roboto', sans-serif;
  position: absolute;
  top: 15%;
  left: 10%;
}

.slider-item-heading {
  color: white;
  font-size: 4rem;
  font-weight: 300;
  text-shadow: 0 1px 1px black;
}

.slider-item-text {
  color: white;
  font-size: 1.8rem;
  text-shadow: 0 1px 1px black;
  background: rgba(0, 0, 0, 0.3);
  padding: 1px 10px;
  box-shadow: 0 0 23px 5px rgba(0, 0, 0, 0.4);
  border-radius: 3px;
  margin-top: 1.5rem;
}

.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition: 0.5s;
}

.slide-right-enter {
  transform: translate(100%, 0);
}
.slide-right-leave {
  transform: translate(-100%, 0);
}

.slide-left-enter {
  transform: translate(-100%, 0);
}
.slide-left-leave {
  transform: translate(100%, 0);
}

@media screen and (max-width: 700px) {
  .slider-item-heading {
    font-size: 3.5rem;
  }

  .slider-item-text {
    font-size: 1.75rem;
  }
}

@media screen and (max-width: 550px) {
  .slider-item-heading {
    font-size: 3rem;
  }

  .slider-item-text {
    font-size: 1.5rem;
  }
}
@media screen and (max-width: 450px) {
  .slider-item-heading {
    font-size: 2.5rem;
  }

  .slider-item-text {
    font-size: 1.25rem;
  }
}
@media screen and (max-width: 320px) {
  .slider-item-heading {
    font-size: 2rem;
  }

  .slider-item-text {
    font-size: 1rem;
  }
}
</style>
