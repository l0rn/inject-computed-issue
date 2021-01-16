<template>
  <Map
    :center="center"
    map-style="mapbox://styles/mapbox/streets-v11"
  >
    <Marker
      :location="{ lat: 53.3764, lng: 9 }"
    />
  </Map>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Map from '@/components/Map.vue'
import Marker from '@/components/Marker.vue'

export default defineComponent({
  name: 'App',
  components: {
    Marker,
    Map
  },
  data() {
    return {
      center: {lat: 53, lng: 9}
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  height: 100%;
  width: 100%;
}

html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}
</style>
