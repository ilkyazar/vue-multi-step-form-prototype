<template>
  <div class="form-footer">
    <button @click="goPrev" v-if="showPrev" class="btn">&laquo; Back</button>
    <button @click="goNext" v-if="showNext" class="btn">Next &raquo;</button>
    <button
      @click="handleSubmit"
      v-if="showSubmit"
      type="submit"
      class="btn submit"
    >
      Submit
    </button>
  </div>
</template>

<script>
export default {
  name: "FormButtonGroup",
  props: {
    showSubmit: {
      type: Boolean,
      default: false,
    },
    showNext: {
      type: Boolean,
      default: false,
    },
    showPrev: {
      type: Boolean,
      default: false,
    },
  },
  methods: {},
  setup(props, { emit }) {
    const goPrev = (event) => {
      emit("goPrev", event.target.value);
    };

    const goNext = (event) => {
      emit("goNext", event.target.value);
    };

    const handleSubmit = (event) => {
      emit("handleSubmit", event.target.value);
    };

    return {
      goPrev,
      goNext,
      handleSubmit,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "@/styles/form-styles.scss";
</style>
