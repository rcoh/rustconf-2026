<script setup lang="ts">
import { onSlideEnter, onSlideLeave, useNav } from '@slidev/client'
import { computed, ref } from 'vue'

type Mode = 'time' | 'gzip'

const props = withDefaults(defineProps<{ mode?: Mode }>(), {
  mode: 'time',
})

const { isPrintMode } = useNav()
const displayedMode = ref<Mode>(props.mode === 'gzip' && isPrintMode.value ? 'gzip' : 'time')
let firstFrame = 0
let secondFrame = 0

const rows = [
  {
    id: 'dial9',
    name: 'dial9',
    small: 'trace format',
    time: { value: '22 ns', width: '2.1%' },
    gzip: { value: '4.7 B/event', width: '16.2%' },
  },
  {
    id: 'json',
    name: 'JSON',
    small: 'tracing + JSON subscriber',
    time: { value: '1,050 ns', width: '100%' },
    gzip: { value: '26.8 B/event', width: '92.4%' },
  },
]

const displayedRows = computed(() => rows.map(row => ({
  ...row,
  width: row[displayedMode.value].width,
})))

function cancelAnimation() {
  cancelAnimationFrame(firstFrame)
  cancelAnimationFrame(secondFrame)
}

function enterSlide() {
  cancelAnimation()

  if (props.mode !== 'gzip' || isPrintMode.value) {
    displayedMode.value = props.mode
    return
  }

  displayedMode.value = 'time'
  firstFrame = requestAnimationFrame(() => {
    secondFrame = requestAnimationFrame(() => {
      displayedMode.value = 'gzip'
    })
  })
}

onSlideEnter(enterSlide)
onSlideLeave(cancelAnimation)
</script>

<template>
  <div class="encode-chart dial9-benchmark">
    <div class="ec-title">Cost to serialize one telemetry event</div>
    <div class="ec-sub ec-mode-copy">
      <span :class="{ 'ec-mode-active': displayedMode === 'time' }">
        wall-clock time to turn one event into bytes &middot; lower is better
      </span>
      <span :class="{ 'ec-mode-active': displayedMode === 'gzip' }">
        gzip level 1 &middot; compressed bytes per event &middot; lower is better
      </span>
    </div>

    <div
      v-for="row in displayedRows"
      :key="row.id"
      :class="['ec-row', `ec-row-${row.id}`]"
    >
      <div class="ec-name">
        {{ row.name }}<br><small>{{ row.small }}</small>
      </div>
      <div class="ec-track">
        <div
          :class="['ec-bar', `ec-bar-${row.id}`]"
          :style="{ width: row.width }"
        ></div>
      </div>
      <div class="ec-val ec-mode-copy">
        <span :class="{ 'ec-mode-active': displayedMode === 'time' }">
          {{ row.time.value }}
        </span>
        <span :class="{ 'ec-mode-active': displayedMode === 'gzip' }">
          {{ row.gzip.value }}
        </span>
      </div>
    </div>

    <div class="ec-src">
      1M-event scheduler-telemetry mix &middot; Apple M2 &middot; medians of 8 runs &middot;
      <a href="https://dial9-rs.github.io/blog/dial9-a-flight-recorder-for-rust/#the-dial9-trace-format">source</a>
    </div>
  </div>
</template>
