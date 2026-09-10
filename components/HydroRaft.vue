<template>
  <div class="hydro-raft">
    <p class="hydro-raft-eyebrow">04 · Hydro</p>
    <h1>Hydro catches consensus bugs</h1>

    <div class="hydro-raft-stage">
      <figure v-click="1" class="hydro-raft-frame">
        <img
          src="/images/hydro-raft-site.png"
          alt="The Raft consensus algorithm website"
        />
        <figcaption>raft.github.io</figcaption>
      </figure>

      <figure v-click="2" class="hydro-raft-frame hydro-raft-frame-overlay">
        <img
          src="/images/hydro-raft-bug.png"
          alt="Google Groups message announcing a bug in Raft membership changes"
        />
        <figcaption>raft-dev · July 2015</figcaption>
      </figure>
    </div>

    <p v-click="3" class="hydro-raft-takeaway">
      Hydro’s simulation tests catch the buggy implementation immediately.
    </p>
  </div>
</template>

<style scoped>
.hydro-raft {
  align-items: center;
  display: flex;
  flex-direction: column;
  height: 100%;
  position: relative;
}

.hydro-raft-eyebrow {
  align-self: flex-start;
  color: var(--rust);
  font-size: 0.82rem;
  font-weight: 760;
  margin: 0;
  text-transform: uppercase;
}

.hydro-raft h1 {
  align-self: flex-start;
  font-size: 2.35rem;
  margin-top: 0.75rem;
}

.hydro-raft-stage {
  height: 18.5rem;
  margin-top: 0.9rem;
  position: relative;
  width: 32.9rem;
}

.hydro-raft-frame {
  background: #fff;
  border: 1px solid var(--line);
  height: 100%;
  inset: 0;
  margin: 0;
  overflow: hidden;
  position: absolute;
  width: 100%;
}

.hydro-raft-frame img {
  display: block;
  height: 100%;
  object-fit: cover;
  width: 100%;
}

.hydro-raft-frame figcaption {
  background: rgba(23, 25, 27, 0.82);
  bottom: 0;
  color: #fff;
  font-size: 0.7rem;
  font-weight: 680;
  left: 0;
  padding: 0.35rem 0.6rem;
  position: absolute;
}

.hydro-raft-frame-overlay {
  z-index: 2;
}

.hydro-raft-takeaway {
  color: var(--rust);
  font-size: 1.08rem;
  font-weight: 720;
  margin: 0.8rem 0 0;
  text-align: center;
}
</style>
