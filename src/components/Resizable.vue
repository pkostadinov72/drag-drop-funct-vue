<template>
  <div ref="resizableElement" class="resizable-element"></div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const resizableElement = ref<HTMLElement | null>(null);

function resizeElement(event: MouseEvent) {
  if (!resizableElement.value) return;
  resizableElement.value.style.width =
    event.clientX - resizableElement.value.offsetLeft + "px";
  resizableElement.value.style.height =
    event.clientY - resizableElement.value.offsetTop + "px";
}

function addEventListeners() {
  document.addEventListener("mousemove", resizeElement);
  document.addEventListener("mouseup", () => {
    document.removeEventListener("mousemove", resizeElement);
  });
}
</script>

<style scoped>
.resizable-element {
  width: 200px;
  height: 200px;
  background-color: limegreen;
  resize: both;
  overflow: auto;
}
</style>
