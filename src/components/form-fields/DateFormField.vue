<template>
  <div class="form-field">
    <label>{{ labelName }}</label>
    <Field
      :name="fieldName"
      type="date"
      class="form-control"
      :class="{ 'is-invalid': error }"
      :value="inputValue"
    />
    <div class="invalid-feedback">{{ error }}</div>
  </div>
</template>

<script>
import { Field } from "vee-validate";

export default {
  name: "DateFormField",
  components: {
    Field,
  },
  props: {
    inputValue: {
      type: String,
      default: "",
    },
    labelName: {
      type: String,
      default: "",
    },
    fieldName: {
      type: String,
      default: "",
    },
    error: {
      type: String,
      default: "",
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/styles/form-styles.scss";
</style>
