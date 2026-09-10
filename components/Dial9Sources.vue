<template>
  <div class="dial9-sources">
    <div v-click="7" class="ds-center">
      <div class="ds-title">dial9</div>
      <div class="ds-sub">all in the same trace</div>
    </div>

    <div v-click="8" class="ds-destination">
      <svg class="ds-destination-arrow" width="24" height="58" aria-hidden="true">
        <path d="M12 0v43m-7-8 7 8 7-8" stroke="currentColor" stroke-width="2" fill="none" />
      </svg>
      <div class="ds-destination-label">Destination support is built into dial9</div>
      <div class="ds-destination-list">
        <span>S3</span>
        <span>local disk</span>
        <span>other destinations</span>
      </div>
    </div>

    <div class="ds-col ds-col-left">
      <div v-click="1" class="ds-item">
        <img src="/images/tokio-logo.svg" class="ds-logo ds-invert" alt="Tokio" />
        <span class="ds-name">Tokio runtime</span>
        <svg class="ds-arrow" width="52" height="20"><path d="M0 10h40m-8-6l8 6-8 6" stroke="currentColor" stroke-width="2" fill="none" /></svg>
      </div>
      <div v-click="3" class="ds-item">
        <img src="/images/tux.svg" class="ds-tux" alt="Linux" />
        <span class="ds-name">Linux kernel</span>
        <svg class="ds-arrow" width="52" height="20"><path d="M0 10h40m-8-6l8 6-8 6" stroke="currentColor" stroke-width="2" fill="none" /></svg>
      </div>
      <div v-click="5" class="ds-item">
        <span class="ds-name ds-metrique">metrique</span>
        <svg class="ds-arrow" width="52" height="20"><path d="M0 10h40m-8-6l8 6-8 6" stroke="currentColor" stroke-width="2" fill="none" /></svg>
      </div>
    </div>

    <div class="ds-col ds-col-right">
      <div v-click="2" class="ds-item">
        <svg class="ds-arrow" width="52" height="20"><path d="M52 10H12m8-6l-8 6 8 6" stroke="currentColor" stroke-width="2" fill="none" /></svg>
        <img src="/images/flamegraph.png" class="ds-flame" alt="Profiling" />
        <span class="ds-name">CPU profiler</span>
      </div>
      <div v-click="4" class="ds-item">
        <svg class="ds-arrow" width="52" height="20"><path d="M52 10H12m8-6l-8 6 8 6" stroke="currentColor" stroke-width="2" fill="none" /></svg>
        <img src="/images/tracing-logo.png" class="ds-tracing" alt="tracing" />
        <span class="ds-name">tracing spans</span>
      </div>
      <div v-click="6" class="ds-item">
        <svg class="ds-arrow" width="52" height="20"><path d="M52 10H12m8-6l-8 6 8 6" stroke="currentColor" stroke-width="2" fill="none" /></svg>
        <span class="ds-name">application events</span>
      </div>
    </div>
  </div>
</template>
