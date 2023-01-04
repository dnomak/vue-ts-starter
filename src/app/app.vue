<script lang="ts">
import { mapStores } from 'pinia'
import { useOptionsStore } from '@/modules/options/store'

export default {
  name: 'App',
  created() {
    this.changeLocale(
      !this.optionsStore.locale ? this.$i18n.locale : this.optionsStore.locale
    )
  },
  computed: {
    ...mapStores(useOptionsStore),
  },
  methods: {
    changeLocale(value: string) {
      this.$i18n.locale = value
      this.optionsStore.changeLocale(value)
    },
  },
}
</script>

<template lang="pug">
div(:class="`route-${$route.name?.toString()}`")
  font-awesome-icon(icon="fa-brands fa-vuejs")
  font-awesome-icon(icon="fa-solid fa-heart")
  font-awesome-icon(icon="fa-regular fa-heart")
  ul
    li
      router-link(to="/") {{ $t('Home') }}
  router-view
  div {{ $t('Language Options') }}:
  ul
    li(v-for="locale in $i18n.availableLocales")
      a(href="#" @click="changeLocale(locale)" :class="{ 'active': optionsStore.locale == locale}") {{ $t('Language', locale) }}
</template>

<style lang="scss" scoped>
.active {
  font-weight: 700;
}
</style>
