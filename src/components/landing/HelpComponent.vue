<template>
  <div class="help-page">
    <nav class="toc">
      <a
        v-for="item in tocItems"
        :key="item.id"
        :href="'#' + item.id"
        :class="{ active: activeSection === item.id }"
        @click.prevent="scrollTo(item.id)"
      >
        {{ item.label }}
      </a>
    </nav>

    <div class="content">
      <section id="creating-workspace" class="help-section">
        <h2>Creating a Workspace</h2>

        <StepItem :number="1" title="Go to Dashboard">
          Click on <strong>Dashboard</strong> in the sidebar to access your workspaces.
          <template #visual>
            <DemoDashboard :highlight-create="true" />
          </template>
        </StepItem>

        <StepItem :number="2" title="Create Workspace">
          Click the <strong>Create a new workspace</strong> button and fill in the workspace details.
          <template #visual>
            <DemoCreateWorkspaceModal />
          </template>
        </StepItem>

        <StepItem :number="3" title="Start Collaborating">
          Your workspace is ready. Invite team members or create projects and channels.
        </StepItem>
      </section>

      <section id="joining-workspace" class="help-section">
        <h2>Joining a Workspace</h2>

        <StepItem :number="1" title="Go to Dashboard">
          Click on <strong>Dashboard</strong> in the sidebar to access your workspaces.
          <template #visual>
            <DemoDashboard :highlight-join="true" />
          </template>
        </StepItem>

        <StepItem :number="2" title="Join Workspace">
          Click the <strong>Join a workspace</strong> button and enter the workspace details.
          <template #visual>
            <DemoJoinWorkspaceModal />
          </template>
        </StepItem>

        <StepItem :number="3" title="Start Collaborating">
          You're now part of the workspace. Create projects and channels to collaborate.
        </StepItem>
      </section>

      <section id="inviting-others" class="help-section">
        <h2>Inviting Others</h2>
        <p>Here's how to invite someone to your workspace:</p>

        <StepItem :number="1" title="Open Invite Modal">
          Click <strong>Invite people</strong> in the sidebar under the Workspace section.
          <template #visual>
            <DemoSidebar :show-theme="true" />
          </template>
        </StepItem>

        <StepItem :number="2" title="Copy the Invite Link">
          Click the <strong>Copy Invite Link</strong> button in the modal.
          <template #visual>
            <DemoModal
              title="Invite people to My Workspace"
              link="https://app.ownly.dev/join/my-workspace..."
            />
          </template>
        </StepItem>

        <StepItem :number="3" title="Send to Your Teammate">
          Share the link with your teammate via chat, email, or any method you prefer.
        </StepItem>

        <StepItem :number="4" title="They Join">
          Your teammate opens the link and clicks <strong>Join</strong> on the dashboard.
        </StepItem>
      </section>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';
import DemoSidebar from './DemoSidebar.vue';
import DemoModal from './DemoModal.vue';
import DemoDashboard from './DemoDashboard.vue';
import DemoCreateWorkspaceModal from './DemoCreateWorkspaceModal.vue';
import DemoJoinWorkspaceModal from './DemoJoinWorkspaceModal.vue';
import StepItem from './StepItem.vue';

const tocItems = [
  { id: 'creating-workspace', label: 'Creating a Workspace' },
  { id: 'joining-workspace', label: 'Joining a Workspace' },
  { id: 'inviting-others', label: 'Inviting Others' },
];

const activeSection = ref('creating-workspace');
let isScrolling = false;

function scrollTo(id: string) {
  const el = document.getElementById(id);
  if (el) {
    activeSection.value = id;
    el.scrollIntoView({ behavior: 'auto' });
  }
}

function handleScroll() {
  if (isScrolling) return;

  const sections = tocItems.map(item => document.getElementById(item.id)).filter(Boolean);
  const scrollPos = window.scrollY + 100;

  for (let i = sections.length - 1; i >= 0; i--) {
    const section = sections[i];
    if (section && section.offsetTop <= scrollPos) {
      activeSection.value = section.id;
      break;
    }
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped lang="scss">
.help-page {
  display: flex;
  gap: 2rem;
  color: inherit;
}

.toc {
  position: sticky;
  top: 2rem;
  align-self: flex-start;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  min-width: 180px;
  padding: 1rem;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 8px;

  a {
    color: inherit;
    text-decoration: none;
    padding: 0.5rem 0.75rem;
    border-radius: 6px;
    font-size: 0.9rem;
    transition: background-color 0.2s;

    &:hover {
      background: rgba(255, 255, 255, 0.1);
    }

    &.active {
      background: rgba(255, 255, 255, 0.15);
      font-weight: 600;
    }
  }
}

.content {
  flex: 1;
  min-width: 0;
}

.help-section {
  margin-bottom: 2.5rem;

  h2 {
    font-size: 1.5rem;
    font-weight: 600;
    color: inherit;
    margin-bottom: 0.75rem;
  }

  > p {
    font-size: 1.15rem;
    font-weight: 300;
    color: inherit;
    line-height: 1.6;
    margin-bottom: 0.5rem;
  }

  strong {
    color: inherit;
    font-weight: 600;
  }

  code {
    background: rgba(255, 255, 255, 0.15);
    padding: 0.15em 0.4em;
    border-radius: 4px;
    font-size: 0.9em;
    color: inherit;
  }
}
</style>
