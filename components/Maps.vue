<script setup>
import { Loader } from "@googlemaps/js-api-loader";

const API_KEY = "AIzaSyDXxld2WqZDKvaRE-QBd_wdHThk1arProk";

let google;
let map;

const props = defineProps({
  markers: Array,
});

onMounted(async () => {
  const loader = new Loader({
    apiKey: API_KEY,
    version: "weekly",
    libraries: ["places", "drawing"],
  });
  const mapOptions = {
    center: {
      lat: 35.68090864020372,
      lng: 139.767681486421,
    },
    zoom: 10,
    gestureHandling: "greedy",
  };

  google = await loader.load();
  google = window.google;
  map = new google.maps.Map(document.getElementById("maps"), mapOptions);
  setupDrawingManager();
});

const markerObjects = computed(() => {
  return props.markers.map((latlng) => {
    new google.maps.Marker({
      position: new google.maps.LatLng(35.539001, 134.228468),
      map: map,
    });
  });
});

const setupDrawingManager = () => {
  const drawingManager = new google.maps.drawing.DrawingManager({
    drawingMode: google.maps.drawing.OverlayType.MARKER,
    drawingControl: true,
    drawingControlOptions: {
      position: google.maps.ControlPosition.TOP_CENTER,
      drawingModes: [
        google.maps.drawing.OverlayType.MARKER,
        google.maps.drawing.OverlayType.CIRCLE,
        google.maps.drawing.OverlayType.POLYGON,
        google.maps.drawing.OverlayType.POLYLINE,
        google.maps.drawing.OverlayType.RECTANGLE,
      ],
    },
  });

  drawingManager.setMap(map);

  new google.maps.event.addListener(drawingManager, "markercomplete", function (marker) {
    props.markers.push({
      lat: marker.getPosition().lat(),
      lng: marker.getPosition().lng(),
    });
  });
};
</script>

<template>
  <div id="maps"></div>
</template>

<style scoped>
#maps {
  width: 100%;
  height: 100%;
}
</style>
