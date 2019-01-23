<template>
  <div
    class="control"
    :class="'control-' + control"
    @click="onSlideChange"
  ></div>
</template>

<script>
export default {
  props: ["control"],

  methods: {
    onSlideChange() {
      this.$emit("slideChange", this.control);
    }
  }
};
</script>

<style scoped>
.control {
  width: 20px;
  height: 20px;
  border: 3px solid white;
  top: 50%;
  transform: translateY(-50%) rotateZ(45deg);
  cursor: pointer;
  position: absolute;
}

.control-right {
  border-bottom-color: transparent;
  border-left-color: transparent;
  right: 4%;
}

.control-left {
  border-top-color: transparent;
  border-right-color: transparent;
  left: 4%;
}
</style>
