<template>
  <div class="demo-dashboard has-background-primary soft-if-dark">
    <div class="demo-inner">
      <section class="hero">
        <div class="hero-body px-5 pb-0 pt-5">
          <p class="title has-text-white">Dashboard</p>
          <p class="subtitle mt-1 has-text-white">
            You can create or join one or more workspaces below
          </p>
        </div>
      </section>

      <div class="spacelist">
        <div class="create card">
          <div class="card-content">
            <div class="block">
              <div class="media-content">
                <p class="subtitle is-5">Don't see what you are looking for?</p>
              </div>
            </div>

            <div class="content has-text-right">
              <button class="button mr-2 mb-2 is-small-caps is-primary soft-if-dark">
                Create a new workspace
              </button>
              <button class="button mr-2 is-small-caps" :class="{ 'is-primary soft-if-dark': highlightJoin }">
                Join a workspace
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps({
  highlightCreate: {
    type: Boolean,
    default: false,
  },
  highlightJoin: {
    type: Boolean,
    default: false,
  },
});
</script>

<style scoped lang="scss">
.demo-dashboard {
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.25);
  overflow: hidden;
}

.demo-inner {
  max-width: 900px;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
}

.spacelist {
  margin: 20px;
}

.card.create {
  box-shadow: none;
}
</style>
