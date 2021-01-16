<template>
  <div
    class="marker"
  />
</template>
<script lang="ts">
import { defineComponent, inject, PropType } from 'vue'
import mapboxgl from 'mapbox-gl'
import { LocationDto } from '@/api/model/LocationDto'
import { MapInject } from './Map.vue'

export default defineComponent({
  name: 'Marker',
  props: {
    location: {
      type: Object as PropType<LocationDto>,
      required: true
    }
  },
  setup() {
    return {
      map: inject(MapInject)
    }
  },
  data() {
    return {
      accessToken: process.env.VUE_APP_MAPBOX_TOKEN,
      marker: new mapboxgl.Marker()
    }
  },
  mounted() {

    this.marker
      .setLngLat([this.location.lng, this.location.lat])
      // The property this.map is now inferred with ComputedRef<mapboxgl.Map> | undefined although the actual value is already unwrapped
      .addTo(this.map)
  }
})

</script>
<style lang="scss" scoped>
.map {
  height: 100%;
  width: 100%;
}
</style>
