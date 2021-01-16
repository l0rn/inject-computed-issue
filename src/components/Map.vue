<template>
  <div
    id="map"
    class="map"
  >
    <slot v-if="map !== null" />
  </div>
</template>
<script lang="ts">
import { defineComponent, computed, provide, InjectionKey, PropType, ref, ComputedRef } from 'vue'
import mapboxgl from 'mapbox-gl'
import { LocationDto } from '@/api/model/LocationDto'

// I would assume that I'd like the type to be InjectionKey<mapboxgl.Map>, but then provide complains
export const MapInject: InjectionKey<ComputedRef<mapboxgl.Map>> = Symbol()

export default defineComponent({
  name: 'Map',
  props: {
    center: {
      type: Object as PropType<LocationDto>,
      required: true
    }
  },
  setup() {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_TOKEN
    const map = ref<mapboxgl.Map | null>(null)

    // inferred type of computed(() => map.value) is obviously ComputedRef<mapboxgl.Map>, but that's not what i want in the injected property (but the unwrapped one)
    provide(MapInject, computed(() => map.value))
    return {
      map,
    }
  },
  mounted() {

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
