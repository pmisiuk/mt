<script setup>
function toggleFullScreen() {
  if (!document.fullscreenElement) {
    document.documentElement.requestFullscreen()
  } else if (document.exitFullscreen) {
    document.exitFullscreen()
  }
}

import { vDraggable } from '@neodrag/vue'
import { computed, ref } from 'vue'
const h = ref(213)
const s = ref(162)
const l = ref(25)

const style = computed(() => `--color: hsl(${h.value},${s.value}%,${l.value}%)`)
</script>

<template>
  <div class="bg" :style="style">
    <div class="controls" v-draggable="{ handle: '.controls__handle' }">
      <div class="controls__handle">
        <button @click="toggleFullScreen" type="button" class="btn">FS</button>
      </div>
      <label class="controls__range">
        <span>H: {{ h }}</span>
        <input v-model="h" type="range" min="0" max="255" step="1" />
      </label>
      <label class="controls__range">
        <span>S: {{ s }}</span>
        <input v-model="s" type="range" min="0" max="255" step="1" />
      </label>
      <label class="controls__range">
        <span>L: {{ l }}</span>
        <input v-model="l" type="range" min="0" max="255" step="1" />
      </label>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.bg {
  background-color: var(--color);
  min-height: 100vh;
  min-height: 100dvh;
  display: grid;
  place-items: center;
}
.controls {
  background-color: rgba(255, 255, 255, 0.5);
  display: grid;
  gap: 1rem;
  padding-bottom: 1rem;

  &__handle {
    display: flex;
    align-items: center;
    justify-content: end;
    background-color: rgba(0, 0, 0, 0.5);
  }

  &__range {
    display: flex;
    align-items: center;
    justify-content: center;
    padding-inline: 1rem;
    gap: 1rem;
    font-size: 1rem;
    font-weight: 700;
  }
}

.btn {
  border: 1px solid rgba(0, 0, 0, 0.5);
}
</style>
