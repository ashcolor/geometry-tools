<script setup>
const props = defineProps({
  markers: Array,
});

const convertArrayToText = computed(() => props.markers.map((latlng) => `${latlng.lat} ${latlng.lng}`).join(",\n"));
const convertArrayToWkt = computed(() => {
  return props.markers.map((latlng) => `POINT('${latlng.lat} ${latlng.lng}')`).join(",\n");
});
</script>
<template>
  <div class="text-container">
    <div class="h-100">
      <div>Array</div>
      <textarea class="wkt__textarea" v-model="convertArrayToText" />
    </div>
    <div class="h-100">
      <div>WKT</div>
      <textarea class="wkt__textarea" v-model="convertArrayToWkt" />
    </div>
    <div class="h-100">
      <div>GeoJson</div>
      <textarea class="wkt__textarea" />
    </div>
  </div>
</template>

<style scoped>
.text-container {
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr;
}
.wkt__textarea {
  width: 100%;
  height: 100%;
}
.h-100 {
  height: 100%;
}
</style>
