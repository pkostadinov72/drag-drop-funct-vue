<template>
  <div
    ref="resizableElement"
    class="resizable-element"
    @mousedown="startResize"
    @mouseup="stopResize"
    @mousemove="doResize"
  >
    <div class="resize-handle"></div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const resizableElement = ref<HTMLElement | null>(null);
let isResizing = false;
let currentWidth = 0;
let currentHeight = 0;
let startX = 0;
let startY = 0;

function startResize(event: MouseEvent) {
  isResizing = true;
  startX = event.clientX;
  startY = event.clientY;
  currentWidth = resizableElement.value
    ? resizableElement.value.offsetWidth
    : 0;
  currentHeight = resizableElement.value
    ? resizableElement.value.offsetHeight
    : 0;
  resizableElement.value?.style.setProperty("user-select", "none");
}

function stopResize() {
  isResizing = false;
  resizableElement.value?.style.removeProperty("user-select");
}

function doResize(event: MouseEvent) {
  if (!isResizing) return;
  if (!resizableElement.value) return;
  const newWidth = currentWidth + (event.clientX - startX);
  const newHeight = currentHeight + (event.clientY - startY);
  resizableElement.value.style.width = `${newWidth}px`;
  resizableElement.value.style.height = `${newHeight}px`;
}
</script>

<style scoped>
.resizable-element {
  width: 200px;
  height: 200px;
  background-color: limegreen;
  resize: both;
  overflow: auto;
  position: relative;
}

.resize-handle {
  width: 10px;
  height: 10px;
  background-color: limegreen;
  position: absolute;
  bottom: 0;
  right: 0;
  cursor: se-resize;
}
</style>
