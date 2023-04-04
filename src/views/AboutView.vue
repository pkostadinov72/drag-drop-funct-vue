<template>
  <div class="about">
    <Dragdroptwo></Dragdroptwo>
  </div>
</template>

<script setup lang="ts">
import Dragdroptwo from "@/components/Dragdroptwo.vue";
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
