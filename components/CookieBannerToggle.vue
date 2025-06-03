<template>
  <div>
    <button @click="showBanner = !showBanner">
      {{ showBanner ? 'Hide Cookie Banner' : 'Show Cookie Banner' }}
    </button>
    <CookieBanner v-model:open="showBanner" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import CookieBanner from './CookieBanner.vue'

const showBanner = ref(false)
</script>