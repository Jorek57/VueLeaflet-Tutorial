<template>
  <l-map
    :center="center"
    :zoom="zoom"
    class="map"
    ref="map"
    @update:zoom="zoomUpdated"
    @update:center="centerUpdated"
  >
    <l-tile-layer
      :url="url"
    >
    </l-tile-layer>
    <l-marker
      v-for="marker in markers"
      :key="marker.id"
      :lat-lng="marker.coordinates"
    >
    </l-marker>
  </l-map>
</template>

<script>
  import { LMap, LTileLayer, LMarker } from 'vue2-leaflet';
  import 'leaflet/dist/leaflet.css';

  export default {
    components: {
      LMap,
      LTileLayer,
      LMarker
    },
    data () {
      return {
        url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
        center: [ 49.1193089, 6.1757156 ],
        zoom: 12,
        markers: [
          {id: 1, coordinates: [ 49.114910, 6.178810 ]},
          {id: 2, coordinates: [ 49.133290, 6.154370 ]},
          {id: 3, coordinates: [ 49.102160, 6.158850 ]},
          {id: 4, coordinates: [ 49.136010, 6.199630 ]},
          {id: 5, coordinates: [ 49.105563, 6.182234 ]},
        ]
      }
    },
    methods: {
      zoomUpdated (zoom) {
        this.zoom = zoom;
        console.log(this.markers)
      },
      centerUpdated (center) {
        this.center = center;
      }
    }
  }
</script>

<style>
  .map {
    position: absolute;
    width: 100%;
    height: 100%;
    overflow :hidden
  }
</style>
