<script lang="ts">
import Options from '@/components/Options.vue'

export default {
  name: 'App',
  components: {
    Options,
  },
}
</script>

<template lang="pug">
div(:class="`route-${$route.name?.toString()}`")
  Options
  font-awesome-icon(icon="fa-brands fa-vuejs")
  font-awesome-icon(icon="fa-solid fa-heart")
  font-awesome-icon(icon="fa-regular fa-heart")
  ul
    li
      router-link(to="/") {{ $t('Home') }}
  router-view
</template>
