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
    <v-marker-cluster
      ref="cluster"
      :averageCenter="true"
      :ignoreHidden="true"
      :options="clusterOptions"
    >
      <restaurant
        v-for="marker in markers"
        :key="marker.id"
        :marker="marker"
      >
      </restaurant>
    </v-marker-cluster>
  </l-map>
</template>

<script>
import Vue from 'vue';
import { Icon, divIcon } from 'leaflet';
import { LMap, LTileLayer } from 'vue2-leaflet';
import Vue2LeafletMarkerCluster from 'vue2-leaflet-markercluster';
import Restaurant from './restaurant';
import ClusterIcon from './cluster-icon'
import 'leaflet/dist/leaflet.css';

const EnhancedClusterIcon = Vue.extend(ClusterIcon);

delete Icon.Default.prototype._getIconUrl;
Icon.Default.mergeOptions({
    iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),
    iconUrl: require('leaflet/dist/images/marker-icon.png'),
    shadowUrl: require('leaflet/dist/images/marker-shadow.png')
})

export default {
  components: {
    LMap,
    LTileLayer,
    Restaurant,
    'v-marker-cluster': Vue2LeafletMarkerCluster
  },
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      center: [ 49.1193089, 6.1757156 ],
      zoom: 12,
      markers: [
        {id: 1, name: 'Restaurant de Poisson', imageUrl: 'https://img.icons8.com/doodle/48/000000/fish-food--v1.png', coordinates: [ 49.114910, 6.178810 ]},
        {id: 2, name: 'Pizzeria', imageUrl: 'https://img.icons8.com/doodle/48/000000/pizza--v1.png' ,coordinates: [ 49.133290, 6.154370 ]},
        {id: 3, name: 'Boulangerie', imageUrl: 'https://img.icons8.com/doodle/48/000000/croissant--v1.png', coordinates: [ 49.102160, 6.158850 ]},
        {id: 4, name: 'Brunch', imageUrl: 'https://img.icons8.com/doodle/48/000000/the-toast--v2.png', coordinates: [ 49.136010, 6.199630 ]},
        {id: 5, name: 'Fast Food', imageUrl: 'https://img.icons8.com/doodle/48/000000/hamburger.png', coordinates: [ 49.105563, 6.182234 ]},
      ],
      clusterOptions: {
          spiderfyDistanceMultiplier: 3,
          iconCreateFunction: cluster => {
              let clusterUsers = cluster.getAllChildMarkers().map(marker => marker.id)
              let clusterIconEl = new EnhancedClusterIcon({propsData: { clusterUsers }}).$mount().$el
              return divIcon({
                  html: clusterIconEl.outerHTML,
                  className: 'cluster',
                  iconSize: null
              })
          }
      }
    }
  },
  methods: {
    zoomUpdated (zoom) {
      this.zoom = zoom;
    },
    centerUpdated (center) {
      this.center = center;
    },
  }
}
</script>

<style>
  @import "~leaflet.markercluster/dist/MarkerCluster.css";
  .map {
    position: absolute;
    width: 100%;
    height: 100%;
    overflow :hidden
  }
  .cluster {
    position: absolute;
    margin-left: -20px;
    margin-top: -20px;
  }
</style>
