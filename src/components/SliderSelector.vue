<template>
  <div
    class="slide-item-selector"
    :class="{ active }"
    @click="$emit('slideSelected')"
  ></div>
</template>

<script>
export default {
  props: ['active']
};
</script>

<style scoped>
.slide-item-selector {
  width: 10px;
  height: 10px;
  border-radius: 10px;
  border: 2px solid white;
  cursor: pointer;
  margin: 0 5px;
}

.active {
  background: #EEE;
}
</style>
