<template>
  <div class="hydro-code">
    <div class="hydro-code-heading">
      <p>04 · Hydro</p>
      <h1>Delivery guarantees are types</h1>
      <span>
        The compiler rejects a fold over a stream that may retry a message.
      </span>
    </div>

    <img
      src="/images/hydro-count-yes.png"
      alt="Hydro compiler error showing that fold requires exactly-once delivery"
    />
  </div>
</template>

<style scoped>
.hydro-code {
  align-items: center;
  display: grid;
  gap: 2.2rem;
  grid-template-columns: 11rem minmax(0, 1fr);
  height: 100%;
}

.hydro-code-heading p {
  color: var(--rust);
  font-size: 0.82rem;
  font-weight: 760;
  margin: 0 0 1.1rem;
  text-transform: uppercase;
}

.hydro-code-heading h1 {
  font-size: 2.45rem;
  line-height: 1.05;
}

.hydro-code-heading span {
  color: var(--muted);
  display: block;
  font-size: 1rem;
  line-height: 1.4;
  margin-top: 1.4rem;
}

.hydro-code > img {
  display: block;
  max-height: 25rem;
  object-fit: contain;
  width: 100%;
}
</style>
