<template>
  <h1 class="form-header">Tax Info</h1>
  <div class="form-body">
    <Form :validation-schema="schema" v-slot="{ errors }">
      <InputFormField
        labelName="Tax ID"
        fieldName="taxId"
        :error="errors.taxId"
        @input="$emit('update:taxId', $event.target.value)"
        :inputValue="taxId"
      />
      <InputFormField
        labelName="Tax Residency"
        fieldName="taxResidency"
        :error="errors.taxResidency"
        @input="$emit('update:taxResidency', $event.target.value)"
        :inputValue="taxResidency"
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
    taxId: {
      type: String,
    },
    taxResidency: {
      type: String,
    },
  },
  setup() {
    const schema = markRaw(
      Yup.object().shape({
        taxId: Yup.string(),
        taxResidency: Yup.string(),
      })
    );
    return { schema };
  },
};
</script>

<style lang="scss" scoped>
@import "@/styles/form-styles.scss";
</style>
