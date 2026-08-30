<template>
  <div class="encode-chart">
    <div class="ec-title">Time to encode one telemetry event</div>
    <div class="ec-sub">wall-clock nanoseconds per event &middot; lower is better</div>

    <div v-click="2" class="ec-row">
      <div class="ec-name">dial9</div>
      <div class="ec-track"><div class="ec-bar ec-bar-dial9"></div></div>
      <div class="ec-val">22 ns</div>
    </div>

    <div v-click="1" class="ec-row">
      <div class="ec-name">JSON<br><small>tracing + JSON subscriber</small></div>
      <div class="ec-track"><div class="ec-bar ec-bar-json"></div></div>
      <div class="ec-val">1,050 ns</div>
    </div>

    <div v-click="3" class="ec-punch">~48&times; faster to emit</div>

    <div class="ec-src">1M-event scheduler-telemetry mix &middot; Apple M2 &middot; medians of 8 runs</div>
  </div>
</template>
