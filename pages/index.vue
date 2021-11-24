<script setup>
const markers = ref([
  {
    lat: 35.68090864020372,
    lng: 139.767681486421,
  },
]);
const polygons = [];
</script>

<template>
  <div class="container">
    <Maps v-model:markers="markers" />
    <Editor v-model:markers="markers" />
  </div>
</template>

<style scoped>
.container {
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-rows: 1fr 1fr;
}
</style>
