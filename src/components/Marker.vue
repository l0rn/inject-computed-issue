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
  setup(props) {
    const map = inject(MapInject)
    const marker = new mapboxgl.Marker()
    onMounted(() => {
      marker
        .setLngLat([props.location.lng, props.location.lat])
        // The property this.map is now inferred with ComputedRef<mapboxgl.Map> | undefined although the actual value is already unwrapped
        .addTo(map!!.value!!)
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
