<template>
  <slot v-if="selectedStep.selectedStepKey === stepKey" :key="stepKey"> </slot>
</template>

<script>
import { inject } from "vue";

export default {
  name: "Step",
  props: ["stepTitle", "stepKey"],
  setup(props) {
    const selectedStep = inject("selectedStep");
    return { ...props, selectedStep };
  },
};
</script>
