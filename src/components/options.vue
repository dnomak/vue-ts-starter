<script lang="ts">
import { mapStores } from 'pinia'

import { useOptionsStore } from '@/stores/options/store'

export default {
  name: 'ComponentOptions',
  created() {
    this.setLocale(!this.optionsStore.locale ? this.$i18n.locale : this.optionsStore.locale)
  },
  computed: {
    ...mapStores(useOptionsStore),
  },
  methods: {
    setLocale(value: string) {
      this.$i18n.locale = value
      this.optionsStore.setLocale(value)
    },
  },
}
</script>

<template lang="pug">
.options
  .options-title {{ $t('LANGUAGE OPTIONS:') }}
  .wrap.xl-2.xl-gutter-8
    .col(v-for="locale in $i18n.availableLocales")
      a.options-item(href="#" @click="setLocale(locale)" :class="{ active: optionsStore.locale == locale }")
        | {{ $t('Language', locale) }}
</template>

<style lang="scss" scoped>
.options {
  position: absolute;
  top: 24rem;
  right: 24rem;
  display: inline-block;
  background-color: var(--white);
  padding: 0 16rem 8rem 16rem;
  border-radius: 8rem;
  width: 100%;
  max-width: 280rem;
  text-align: center;
}
.options-title {
  color: var(--gray-500);
  font-size: 12rem;
  line-height: 1.5;
  font-weight: 700;
  padding-top: 16rem;
  padding-bottom: 8rem;
  text-transform: uppercase;
}
.options-item {
  display: block;
  cursor: pointer;
  padding: 8rem;
  border: 2rem solid var(--gray-300);
  border-radius: 4rem;
  font-weight: 700;
  text-align: center;
  font-size: 14rem;
  line-height: 1.5;
  margin-bottom: 8rem;
  &.active {
    background-color: var(--gray-300);
  }
}
</style>
