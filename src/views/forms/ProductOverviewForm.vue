<template>
  <h1 class="form-header">Product Overview</h1>
  <div class="form-body">
    <Form :validation-schema="schema" v-slot="{ errors }">
      <InputFormField
        labelName="Conditions"
        fieldName="conditions"
        :error="errors.conditions"
        @input="$emit('update:conditions', $event.target.value)"
        :inputValue="conditions"
      />
      <InputFormField
        labelName="Product features"
        fieldName="productFeatures"
        :error="errors.productFeatures"
        @input="$emit('update:productFeatures', $event.target.value)"
        :inputValue="productFeatures"
      />
    </Form>
  </div>
</template>

<script>
import { Form } from "vee-validate";
import * as Yup from "yup";
import { markRaw } from "vue";
import InputFormField from "@/components/form-fields/InputFormField.vue";

export default {
  name: "ProductOverviewForm",
  components: {
    Form,
    InputFormField,
  },
  props: {
    conditions: {
      type: String,
    },
    productFeatures: {
      type: String,
    },
  },
  setup() {
    const schema = markRaw(
      Yup.object().shape({
        conditions: Yup.string(),
        productFeatures: Yup.string(),
      })
    );
    return { schema };
  },
};
</script>

<style lang="scss" scoped>
@import "@/styles/form-styles.scss";
</style>
