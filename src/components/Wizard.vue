<template>
  <div class="steps has-content-centered">
    <div
      v-for="step in steps"
      :key="step.key"
      :class="getClassname(step.key)"
      @click="changeStep(step.key)"
    >
      <span class="steps-marker"></span>
      <div class="steps-content">
        <p class="is-size-4">{{ step.title }}</p>
      </div>
    </div>
  </div>
  <div class="form-content">
    <form @submit.prevent="handleSubmit">
      <slot :key="selectedStep.selectedStepKey"></slot>
      <FormButtonGroup
        :showNext="!stepBools.isLastStep"
        :showPrev="!stepBools.isFirstStep"
        :showSubmit="stepBools.isLastStep"
        v-on:goPrev="goPrev"
        v-on:goNext="goNext"
        v-on:handleSubmit="handleSubmit"
      ></FormButtonGroup>
    </form>
  </div>
</template>

<script>
import { ref, reactive, provide, onMounted, toRef } from "vue";
import FormButtonGroup from "@/components/FormButtonGroup.vue";

export default {
  name: "Wizard",
  components: {
    FormButtonGroup,
  },
  props: {
    formData: Object,
  },
  emits: ["submit"],
  setup(props, { slots, emit }) {
    const data = toRef(props, "formData");
    const steps = ref([]);
    const selectedStep = reactive({ selectedStepKey: null });
    provide("selectedStep", selectedStep);
    const stepBools = ref({ isFirstStep: false, isLastStep: false });

    onMounted(() => {
      steps.value = slots.default().map((step) => {
        if (step.props && step.props["stepKey"]) {
          return {
            key: step.props["stepKey"],
            title: step.props["stepTitle"],
          };
        }
      });
      selectedStep.selectedStepKey = steps.value[0]?.key;
      stepBools.value.isFirstStep = true;
      stepBools.value.isLastStep = false;
    });

    const changeStep = (newKey) => {
      selectedStep.selectedStepKey = newKey;
      updateStepBools();
    };

    const changeStepWithIndex = (index) => {
      selectedStep.selectedStepKey = steps.value[index]?.key;
      updateStepBools();
    };

    const updateStepBools = () => {
      stepBools.value.isFirstStep =
        steps.value[0]?.key == selectedStep.selectedStepKey;
      stepBools.value.isLastStep =
        steps.value[steps.value.length - 1]?.key ==
        selectedStep.selectedStepKey;
    };

    const getCurrentIndex = () => {
      return steps.value
        .map((step) => step.key)
        .indexOf(selectedStep.selectedStepKey);
    };

    const goPrev = () => {
      changeStepWithIndex(getCurrentIndex() - 1);
    };

    const goNext = () => {
      changeStepWithIndex(getCurrentIndex() + 1);
    };

    const isStepActive = (key) => {
      return key === selectedStep.selectedStepKey;
    };

    const getClassname = (key) => {
      return [
        "steps-segment",
        {
          "steps-segment is-active": isStepActive(key),
        },
      ];
    };

    function handleSubmit() {
      emit("submit", data.value);
    }

    return {
      steps,
      selectedStep,
      changeStep,
      getClassname,
      stepBools,
      goPrev,
      goNext,
      handleSubmit,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../../node_modules/bulma-steps-component/bulma/bulma.sass";
@import "../../node_modules/bulma-steps-component/bulma-steps.sass";
</style>
