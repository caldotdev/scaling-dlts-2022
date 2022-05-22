<script setup lang="ts">
import { computed } from "vue";
import { handleBackground } from "../node_modules/slidev-theme-academic/layout-helper";

const props = defineProps({
  image: {
    type: String,
  },
  class: {
    type: String,
  },
});
const style = computed(() => handleBackground(props.image));
</script>

<template>
  <div class="grid grid-cols-2 w-full h-full">
    <div class="slidev-layout default" :class="props.class">
      <slot />
    </div>
    <div class="w-full w-full bg" :style="style" />
  </div>
</template>

<style scoped>
.bg {
    background-size: contain !important;
    margin-top: 2.5rem;
    margin-bottom: 2.5rem;
}

</style>