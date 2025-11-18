<template>
  <div class="text-h3">
    <p class="text-h6 text-weight-light">{{ store.aboutContent }}</p>
  </div>
</template>
<script setup>
import useDefaultStore from '@/stores/defaultStore.js';

const store = useDefaultStore();
</script>
