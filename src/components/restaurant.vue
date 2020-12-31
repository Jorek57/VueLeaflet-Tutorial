<template>
  <l-marker
    :key="marker.id"
    :lat-lng="marker.coordinates"
  >
    <l-icon ref="icon">
      <img class="restaurant-icon" :src="marker.imageUrl"/>
    </l-icon>
    <l-popup>
      <h3>{{ marker.name }}</h3>
      <p>{{ marker.grade }}</p>
    </l-popup>
  </l-marker>
</template>

<script>
import { LIcon, LMarker, LPopup } from 'vue2-leaflet'
export default {
  components: { LIcon, LMarker, LPopup },
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
    margin-left: -15px;
    width: auto;
  }
</style>
