<template>
  <div />
</template>
<script lang="ts">
import { defineComponent, inject, onMounted, PropType } from 'vue'
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
  inject: { map: MapInject },
  mounted() {
    const marker = new mapboxgl.Marker()
    marker
      .setLngLat([this.location.lng, this.location.lat])
      // @ts-ignore type inference does not work!
      .addTo(this.map.value)

  }
})

</script>
<style lang="scss" scoped>
.map {
  height: 100%;
  width: 100%;
}
</style>
