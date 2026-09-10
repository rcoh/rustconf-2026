<template>
  <div class="battery-pack-details">
    <p class="battery-pack-eyebrow">05 · Battery Packs</p>

    <div class="battery-pack-grid">
      <div>
        <h1>Shared ecosystem knowledge</h1>
        <p class="battery-pack-explanation">
          One command applies a curated set of crates for a domain.
        </p>
      </div>

      <pre aria-label="Battery Pack command"><code>cargo bp add embedded</code></pre>
    </div>

    <p class="battery-pack-thesis">
      The larger proposal connects crate discovery with sustained maintenance
      and company sponsorship.
    </p>
  </div>
</template>

<style scoped>
.battery-pack-details {
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: space-between;
  padding: 0.1rem 0 1.2rem;
}

.battery-pack-eyebrow {
  color: var(--rust);
  font-size: 0.82rem;
  font-weight: 760;
  margin: 0;
  text-transform: uppercase;
}

.battery-pack-grid {
  align-items: center;
  display: grid;
  gap: 4rem;
  grid-template-columns: minmax(0, 1fr) minmax(20rem, 0.9fr);
}

.battery-pack-grid h1 {
  color: var(--ink);
  font-size: 3.3rem;
  line-height: 1.05;
  max-width: 28rem;
}

.battery-pack-explanation {
  color: var(--muted);
  font-size: 1.45rem;
  line-height: 1.35;
  margin: 2rem 0 0;
  max-width: 27rem;
}

.battery-pack-grid pre {
  background: var(--dark);
  border-left: 8px solid var(--rust);
  border-radius: 0;
  color: #fff;
  font-size: 1.35rem;
  line-height: 1.5;
  margin: 0;
  padding: 2rem 2.2rem;
}

.battery-pack-grid code {
  background: transparent;
  color: inherit;
  font-size: inherit;
}

.battery-pack-thesis {
  border-top: 1px solid var(--line);
  color: var(--ink);
  font-size: 1.5rem;
  font-weight: 680;
  line-height: 1.3;
  margin: 0;
  max-width: 48rem;
  padding-top: 1.2rem;
}
</style>
