<template>
    <div>
        <l-map
            class="map"
            ref="map"
        >
            <l-tile-layer
                :url="url"
            >
            </l-tile-layer>
        </l-map>
        <h1>Here comes the map</h1>
    </div>
</template>

<script>
import { LMap, LTileLayer, } from 'vue2-leaflet';
import 'leaflet/dist/leaflet.css';

export default {
    components: {
        LMap,
        LTileLayer,
    },
    data () {
        return {
            url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
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
