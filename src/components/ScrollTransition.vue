<template>
  <component
    :is="as"
    ref="el"
    :class="[
      'transition-all duration-500',
      moreDelay ? 'delay-500' : 'delay-300',
      trueCount < 1 && translateEffect
        ? isVisible
          ? transtionPosition[transition].from
          : transtionPosition[transition].to
        : '',
      trueCount < 1 && opacityEffect
        ? isVisible
          ? 'opacity-100'
          : 'opacity-0'
        : '',
    ]"
  >
    <slot />
  </component>
</template>

<script setup lang="ts">
import { ref, watchEffect } from "vue";
import { useElementVisibility } from "@vueuse/core";

type ObjectKeyPair = {
  [key: string]: {
    [key: string]: string;
  };
};

const el = ref(null);
const isVisible = useElementVisibility(el);
const trueCount = ref(0);

watchEffect(() => {
  if (isVisible.value && trueCount.value < 1) {
    trueCount.value++;
  }
});

const transtionPosition: ObjectKeyPair = {
  vertical: { from: "translate-y-0", to: "translate-y-12" },
  horizontalToRight: { from: "-translate-x-0", to: "-translate-x-12" },
  horizontalToLeft: { from: "translate-x-0", to: "translate-x-12" },
};

type TransitionTypes = {
  translateEffect?: boolean;
  opacityEffect?: boolean;
  moreDelay?: boolean;
  transition?: "vertical" | "horizontalToRight" | "horizontalToLeft";
  as?: string;
};

withDefaults(defineProps<TransitionTypes>(), {
  translateEffect: true,
  opacityEffect: true,
  moreDelay: false,
  transition: "vertical",
  as: "div",
});
</script>
