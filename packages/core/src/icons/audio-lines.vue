<script setup lang="ts">
import { ref } from "vue";

defineProps({
  size: { type: Number, default: 28 },
  color: { type: String, default: "currentColor" },
  strokeWidth: { type: Number, default: 2 },
  className: { type: String, default: "" },
  active: { type: Boolean, default: false },
});

const isAnimating = ref(false);
const isControlled = ref(false);

function startAnimation() {
  isControlled.value = true;
  isAnimating.value = true;
}

function stopAnimation() {
  isControlled.value = true;
  isAnimating.value = false;
}

defineExpose({ startAnimation, stopAnimation });

function handleMouseEnter() {
  if (!isControlled.value) isAnimating.value = true;
}

function handleMouseLeave() {
  if (!isControlled.value) isAnimating.value = false;
}
</script>

<template>
  <div
    class="audio-lines-icon"
    :class="[className]"
    v-bind="$attrs"
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      fill="none"
      :height="size"
      :stroke="color"
      stroke-linecap="round"
      stroke-linejoin="round"
      :stroke-width="strokeWidth"
      viewBox="0 0 24 24"
      :width="size"
      :class="{ animating: isAnimating || active }"
    >
      <path d="M2 10v3" />
      <path
        class="line-1"
        d="M6 6v11"
      />
      <path
        class="line-2"
        d="M10 3v18"
      />
      <path
        class="line-3"
        d="M14 8v7"
      />
      <path
        class="line-4"
        d="M18 5v13"
      />
      <path d="M22 10v3" />
    </svg>
  </div>
</template>

<style scoped>
.audio-lines-icon {
  display: inline-flex;
}

.audio-lines-icon svg.animating .line-1 {
  animation: line-1-anim 1.5s ease-in-out infinite;
}

.audio-lines-icon svg.animating .line-2 {
  animation: line-2-anim 1s ease-in-out infinite;
}

.audio-lines-icon svg.animating .line-3 {
  animation: line-3-anim 0.8s ease-in-out infinite;
}

.audio-lines-icon svg.animating .line-4 {
  animation: line-4-anim 1.5s ease-in-out infinite;
}

@keyframes line-1-anim {
  0%, 100% {
    d: path("M6 6v11");
  }
  50% {
    d: path("M6 10v3");
  }
}

@keyframes line-2-anim {
  0%, 100% {
    d: path("M10 3v18");
  }
  50% {
    d: path("M10 9v5");
  }
}

@keyframes line-3-anim {
  0%, 100% {
    d: path("M14 8v7");
  }
  50% {
    d: path("M14 6v11");
  }
}

@keyframes line-4-anim {
  0%, 100% {
    d: path("M18 5v13");
  }
  50% {
    d: path("M18 7v9");
  }
}
</style>
