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
    <restaurant
      v-for="marker in markers"
      :key="marker.id"
      :marker="marker"
    >
    </restaurant>
  </l-map>
</template>

<script>
import { LMap, LTileLayer } from 'vue2-leaflet';
import Restaurant from './restaurant'
import 'leaflet/dist/leaflet.css';

export default {
  components: {
    LMap,
    LTileLayer,
    Restaurant
  },
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      center: [ 49.1193089, 6.1757156 ],
      zoom: 12,
      markers: [
        {id: 1, imageUrl: 'https://img.icons8.com/doodle/48/000000/fish-food--v1.png', coordinates: [ 49.114910, 6.178810 ]},
        {id: 2, imageUrl: 'https://img.icons8.com/doodle/48/000000/pizza--v1.png' ,coordinates: [ 49.133290, 6.154370 ]},
        {id: 3, imageUrl: 'https://img.icons8.com/doodle/48/000000/croissant--v1.png', coordinates: [ 49.102160, 6.158850 ]},
        {id: 4, imageUrl: 'https://img.icons8.com/doodle/48/000000/the-toast--v2.png', coordinates: [ 49.136010, 6.199630 ]},
        {id: 5, imageUrl: 'https://img.icons8.com/doodle/48/000000/hamburger.png', coordinates: [ 49.105563, 6.182234 ]},
      ]
    }
  },
  methods: {
    zoomUpdated (zoom) {
      this.zoom = zoom;
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
