<script setup lang="ts">
import { useSlideContext } from '@slidev/client'

const { $frontmatter } = useSlideContext()

const sections = [
  { id: 'intro', label: 'Intro' },
  { id: 'metrique', label: 'metrique' },
  { id: 'dial9', label: 'dial9' },
  { id: 'testing', label: 'shuttle/turmoil' },
  { id: 'hydro', label: 'hydro' },
  { id: 'battery', label: 'batterypacks' },
]
</script>

<template>
  <footer
    v-if="$frontmatter.footer !== false"
    class="deck-signpost"
    aria-label="Talk sections"
  >
    <nav class="deck-signpost-nav">
      <template v-for="(section, index) in sections" :key="section.id">
        <span
          :class="[
            'deck-signpost-section',
            { 'deck-signpost-section-active': $frontmatter.section === section.id },
          ]"
        >
          {{ section.label }}
        </span>
        <span
          v-if="index < sections.length - 1"
          class="deck-signpost-separator"
          aria-hidden="true"
        >
          |
        </span>
      </template>
    </nav>

    <div class="deck-signpost-qr-block">
      <span class="deck-signpost-url">rust-at-aws.github.io</span>
      <div class="deck-signpost-qr-wrap">
        <a
          class="deck-signpost-qr"
          href="https://rust-at-aws.github.io/"
          aria-label="Open Rust at AWS"
        >
          <img src="/images/qr-rust-at-aws.svg" alt="" />
        </a>
        <span
          v-if="$frontmatter.qrCircle"
          v-click
          class="deck-signpost-qr-ring"
          aria-hidden="true"
        ></span>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.deck-signpost {
  align-items: end;
  bottom: 0.55rem;
  display: grid;
  gap: 1rem;
  grid-template-columns: minmax(0, 1fr) max-content;
  left: 4.2rem;
  pointer-events: none;
  position: absolute;
  right: 1.2rem;
  z-index: 40;
}

.deck-signpost-nav {
  align-items: center;
  border-top: 1px solid var(--line);
  display: flex;
  gap: 0.55rem;
  height: 2.75rem;
  white-space: nowrap;
}

.deck-signpost-section {
  color: var(--muted);
  font-size: 0.68rem;
  font-weight: 680;
  position: relative;
}

.deck-signpost-section-active {
  color: var(--rust);
  font-weight: 820;
}

.deck-signpost-section-active::before {
  background: var(--rust);
  content: "";
  height: 3px;
  left: 0;
  position: absolute;
  right: 0;
  top: -1.47rem;
}

.deck-signpost-separator {
  color: var(--line);
  font-size: 0.72rem;
}

.deck-signpost-qr-wrap {
  height: 3rem;
  position: relative;
  width: 3rem;
}

.deck-signpost-qr-block {
  align-items: center;
  display: flex;
  gap: 0.65rem;
  pointer-events: auto;
}

.deck-signpost-url {
  color: var(--muted);
  font-size: 0.68rem;
  font-weight: 500;
  white-space: nowrap;
}

.deck-signpost-qr {
  background: #fff;
  border: 1px solid var(--line);
  display: block;
  height: 3rem;
  padding: 0.18rem;
  position: relative;
  width: 3rem;
  z-index: 2;
}

.deck-signpost-qr img {
  display: block;
  height: 100%;
  width: 100%;
}

.deck-signpost-qr-ring {
  border: 3px solid var(--rust);
  border-radius: 50%;
  inset: -0.5rem;
  pointer-events: none;
  position: absolute;
  rotate: -7deg;
  scale: 1;
  transition:
    opacity 180ms ease,
    rotate 520ms cubic-bezier(0.22, 1, 0.36, 1),
    scale 520ms cubic-bezier(0.22, 1, 0.36, 1);
  z-index: 3;
}

.deck-signpost-qr-ring.slidev-vclick-hidden {
  rotate: -35deg;
  scale: 0.55;
}
</style>
