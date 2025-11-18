<template>
  <q-header class="bg-white text-black">
    <q-toolbar class="row items-center justify-between">
      <div class="col row items-center">
        <!-- <q-btn class="" dense flat round icon="r_menu" @click="$emit('toggleLeftDrawer')" /> -->
        <span class="q-ml-sm text-overline">HOME</span>
        <span class="q-ml-sm text-overline">ABOUT</span>
      </div>

      <q-toolbar-title class="col row justify-center">
        <span class="text-weight-bold text-h5 text-center"> T E K T E K </span>
      </q-toolbar-title>

      <div class="col"></div>
    </q-toolbar>
  </q-header>
</template>

<script setup>
defineEmits(['toggleLeftDrawer']);
</script>

<style scoped>
.rotate-on-hover {
  transform: rotate(0);
  transition: transform 0.8s ease-in-out;
}
.rotate-on-hover:hover {
  transform: rotate(-360deg);
  transition: transform 0.8s ease-in-out;
}
</style>
