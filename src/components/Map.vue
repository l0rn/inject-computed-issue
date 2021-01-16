<template>
  <div
    id="map"
    class="map"
  >
    <slot v-if="initialized" />
  </div>
</template>
<script lang="ts">
import { defineComponent, computed, provide, onMounted, InjectionKey, PropType, ref, ComputedRef } from 'vue'
import mapboxgl from 'mapbox-gl'
import { LocationDto } from '@/api/model/LocationDto'

// I would assume that I'd like the type to be InjectionKey<mapboxgl.Map>, but then provide complains
export const MapInject: InjectionKey<ComputedRef<mapboxgl.Map | null>> = Symbol()

export default defineComponent({
  name: 'Map',
  props: {
    center: {
      type: Object as PropType<LocationDto>,
      required: true
    }
  },
  setup(props) {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_TOKEN
    const map = ref<mapboxgl.Map | null>(null)
    const initialized = ref(false)

    // inferred type of computed(() => map.value) is obviously ComputedRef<mapboxgl.Map>, but that's not what i want in the injected property (but the unwrapped one)
    provide(MapInject, computed(() => map.value))

    onMounted(() => {
      map.value = new mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/mapbox/streets-v11',
        center: [props.center.lng, props.center.lat],
        zoom: 5
      })
      map.value.on('load', () => {
        initialized.value = true
      })
    })
    return {
      map,
      initialized
    }
  }
})

</script>
<style lang="scss" scoped>
.map {
  height: 100%;
  width: 100%;
}
</style>
