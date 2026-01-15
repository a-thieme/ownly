<template>
  <div v-if="paused" class="modal-overlay">
    <div class="modal-box">
      <h3>Ownly is open in another tab</h3>
      <p>The connection was moved to a new tab. Click below or reload this tab to use ownly here instead.</p>
      <button class="button is-primary" @click="resumeHere">Resume Here</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';
import { GlobalBus } from '@/services/event-bus';

const paused = ref(false);

const onPaused = () => {
  paused.value = true;
};

const resumeHere = () => {
  window.location.reload();
};

onMounted(() => {
  // Listen for the pause event
  GlobalBus.addListener('app-paused', onPaused);
});

onUnmounted(() => {
  // Clean up listener to prevent memory leaks
  GlobalBus.removeListener('app-paused', onPaused);
});
</script>

<style scoped lang="scss">
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100dvh;
  background-color: rgba(0, 0, 0, 0.6);
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(2px);

  .modal-box {
    background: var(--bg-color, #fff);
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
    text-align: center;
    max-width: 400px;

    h3 {
      font-size: 1.25rem;
      font-weight: 600;
      margin-bottom: 0.5rem;
      color: var(--text-color);
    }

    p {
      margin-bottom: 1.5rem;
      color: var(--text-color-light);
    }
  }
}
</style>
