<script setup lang="ts">
import { onMounted } from 'vue';
import HelpComponent from '@/components/landing/HelpComponent.vue';
import { formTabName } from '@/utils';

onMounted(() => {
  document.title = formTabName('Getting Started');
});
</script>

<template>
  <main class="has-background-primary soft-if-dark">
    <div class="help-content">
      <h1 class="title">Help</h1>
      <HelpComponent />
    </div>
  </main>
</template>

<style scoped lang="scss">
main {
  overflow-y: auto;
  height: 100%;
}

.help-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem 1rem;
  color: white;
}

.title {
  color: white;
  text-align: center;
  margin-bottom: 2rem;
}
</style>
