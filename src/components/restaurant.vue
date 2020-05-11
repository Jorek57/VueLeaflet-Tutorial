<template>
  <l-marker
    :key="marker.id"
    :lat-lng="marker.coordinates"
  >
    <l-icon ref="icon">
      <img class="restaurant-icon" :src="marker.imageUrl"/>
    </l-icon>
  </l-marker>
</template>

<script>
import { LIcon, LMarker } from 'vue2-leaflet'
export default {
  components: { LIcon, LMarker },
  props: {
    marker: {
      type: Object,
      required: true
    }
  }
}

</script>

<style>
  .restaurant-icon {
    height: 50px;
    width: auto;
  }
</style>
