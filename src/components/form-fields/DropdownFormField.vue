<template>
  <div class="form-field">
    <label>{{ labelName }}</label>
    <Field
      :name="fieldName"
      as="select"
      class="form-control"
      :class="{ 'is-invalid': error }"
    >
      <option value>{{ inputValue }}</option>
      <option v-for="option in options" :key="option" :value="option">
        {{ option }}
      </option>
    </Field>
    <div class="invalid-feedback">{{ error }}</div>
  </div>
</template>

<script>
import { Field } from "vee-validate";

export default {
  name: "DropdownFormField",
  components: {
    Field,
  },
  props: {
    inputValue: {
      type: String,
      default: "",
    },
    options: {
      type: Array,
      default: () => [],
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
