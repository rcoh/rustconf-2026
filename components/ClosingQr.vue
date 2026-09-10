<template>
  <div class="closing-qr">
    <img
      src="/images/qr-rust-at-aws.svg"
      alt="QR code for rust-at-aws.github.io"
    />
    <span>rust-at-aws.github.io</span>
  </div>
</template>

<style scoped>
:global(.slidev-layout.closing-qr-slide) {
  padding: 0.7rem;
}

.closing-qr {
  align-items: center;
  color: var(--ink);
  display: flex;
  flex-direction: column;
  gap: 0.45rem;
  height: 100%;
  justify-content: center;
}

.closing-qr img {
  display: block;
  height: 29rem;
  max-height: calc(100% - 2rem);
  max-width: 94%;
  width: 29rem;
}

.closing-qr span {
  color: var(--rust);
  font-size: 0.95rem;
  font-weight: 760;
}
</style>
