<template>
  <div
    id="map"
    class="map"
  >
    <slot v-if="map !== null" />
  </div>
</template>
<script lang="ts">
import { defineComponent, PropType, computed } from 'vue'
import mapboxgl from 'mapbox-gl'
import { LocationDto } from '@/api/model/LocationDto'

// I would assume that I'd like the type to be InjectionKey<mapboxgl.Map>, but the
export const MapInject = Symbol()

export default defineComponent({
  name: 'Map',
  props: {
    center: {
      type: Object as PropType<LocationDto>,
      required: true
    }
  },
  provide() {
    return {
      [MapInject]: computed(() => this.map)
    }
  },
  data() {
    return {
      map: null as mapboxgl.Map | null
    }
  },
  mounted() {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_TOKEN
    const map = new mapboxgl.Map({
      container: 'map',
      style: 'mapbox://styles/mapbox/streets-v11',
      center: [this.center.lng, this.center.lat],
      zoom: 5
    })
    map.on('load', () => {
      this.map = map
    })
  }
})

</script>
<style lang="scss" scoped>
.map {
  height: 100%;
  width: 100%;
}
</style>
