<template>
  <div class="battery-pack-intro">
    <div class="battery-pack-copy">
      <div>
        <p class="battery-pack-eyebrow">05 · One last thing</p>
        <h1>Battery Packs</h1>
        <p class="battery-pack-subtitle">
          A shared answer to “which crates should I use?”
        </p>
      </div>

      <div class="battery-pack-source">
        <a href="https://github.com/battery-pack-rs/battery-pack">
          github.com/battery-pack-rs/battery-pack
        </a>
        <span>Idea and original slides by Niko Matsakis</span>
      </div>
    </div>

    <img
      src="/images/battery-pack-logo.png"
      alt="Battery Pack logo with Ferris between two batteries"
      class="battery-pack-logo"
    />
  </div>
</template>

<style scoped>
.battery-pack-intro {
  align-items: center;
  display: grid;
  gap: 3rem;
  grid-template-columns: minmax(0, 1fr) 21rem;
  height: 100%;
}

.battery-pack-copy {
  align-self: stretch;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 3.4rem 0 2.8rem;
}

.battery-pack-eyebrow {
  color: var(--rust);
  font-size: 0.82rem;
  font-weight: 760;
  margin: 0 0 2rem;
  text-transform: uppercase;
}

.battery-pack-copy h1 {
  color: var(--rust);
  font-size: 5.6rem;
  line-height: 0.96;
  max-width: 30rem;
}

.battery-pack-subtitle {
  color: var(--ink);
  font-size: 1.75rem;
  line-height: 1.25;
  margin: 2.2rem 0 0;
  max-width: 30rem;
}

.battery-pack-source {
  align-items: flex-start;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.battery-pack-source a {
  border-bottom: 1px solid currentColor;
  font-size: 0.82rem;
  font-weight: 680;
  padding-bottom: 0.15rem;
}

.battery-pack-source span {
  color: var(--muted);
  font-size: 0.78rem;
}

.battery-pack-logo {
  height: 21rem;
  object-fit: contain;
  width: 21rem;
}
</style>
