<template>
  <h2 class="form-header">Personal Info</h2>
  <div class="form-body">
    <Form :validation-schema="schema" v-slot="{ errors }">
      <InputFormField
        labelName="First Name"
        fieldName="firstName"
        :error="errors.firstName"
        @input="$emit('update:firstName', $event.target.value)"
        :inputValue="firstName"
      />
      <InputFormField
        labelName="Last Name"
        fieldName="lastName"
        :error="errors.lastName"
        @input="$emit('update:lastName', $event.target.value)"
        :inputValue="lastName"
      />
      <DateFormField
        labelName="Birthday"
        fieldName="birthday"
        :error="errors.birthday"
        @input="$emit('update:birthday', $event.target.value)"
        :inputValue="birthday"
      />
      <InputFormField
        labelName="Birth Place"
        fieldName="birthPlace"
        :error="errors.birthPlace"
        @input="$emit('update:birthPlace', $event.target.value)"
        :inputValue="birthPlace"
      />
      <DropdownFormField
        :options="countryOfBirthOptions"
        labelName="Country of Birth"
        fieldName="countryOfBirth"
        :error="errors.countryOfBirth"
        @input="$emit('update:countryOfBirth', $event.target.value)"
        :inputValue="countryOfBirth"
      />
      <DropdownFormField
        :options="genderOptions"
        labelName="Gender"
        fieldName="gender"
        :error="errors.gender"
        @input="$emit('update:gender', $event.target.value)"
        :inputValue="gender"
      />
      <DropdownFormField
        :options="nationalityOptions"
        labelName="Nationality"
        fieldName="nationality"
        :error="errors.nationality"
        @input="$emit('update:nationality', $event.target.value)"
        :inputValue="nationality"
      />
      <DropdownFormField
        :options="secondNationalityOptions"
        labelName="Second Nationality"
        fieldName="secondNationality"
        :error="errors.secondNationality"
        @input="$emit('update:secondNationality', $event.target.value)"
        :inputValue="secondNationality"
      />
    </Form>
  </div>
</template>

<script>
import { Form } from "vee-validate";
import * as Yup from "yup";
import { markRaw } from "vue";
import InputFormField from "@/components/form-fields/InputFormField.vue";
import DropdownFormField from "@/components/form-fields/DropdownFormField.vue";
import DateFormField from "@/components/form-fields/DateFormField.vue";
import { ref } from "vue";

export default {
  name: "PersonalInfoForm",
  components: {
    Form,
    InputFormField,
    DropdownFormField,
    DateFormField,
  },
  props: {
    formData: {
      type: Object,
      required: true,
    },
    firstName: {
      type: String,
    },
    lastName: {
      type: String,
    },
    birthday: {
      type: String,
    },
    birthPlace: {
      type: String,
    },
    countryOfBirth: {
      type: String,
    },
    gender: {
      type: String,
    },
    nationality: {
      type: String,
    },
    secondNationality: {
      type: String,
    },
  },
  setup() {
    const schema = markRaw(
      Yup.object().shape({
        firstName: Yup.string().required("First name is required"),
        lastName: Yup.string().required("Last name is required"),
        birthday: Yup.string()
          .required("Birthday is required")
          .matches(
            /^\d{4}-(0[1-9]|1[012])-(0[1-9]|[12][0-9]|3[01])$/,
            "Date of Birth must be a valid date in the format YYYY-MM-DD"
          ),
        birthPlace: Yup.string().required("Birth Place is required"),
        countryOfBirth: Yup.string().required("Country of Birth is required"),
        gender: Yup.string().required("Gender is required"),
        nationality: Yup.string().required("Nationality is required"),
        secondNationality: Yup.string(),
      })
    );
    const countryOfBirthOptions = ref(["Germany", "Belgium", "Netherlands"]);
    const genderOptions = ref(["not specified", "female", "male", "diverse"]);
    const nationalityOptions = ref(["German", "Turkish"]);
    const secondNationalityOptions = ref(["German", "Turkish"]);
    const sectionOptions = ref(["keine Eingabe"]);
    return {
      schema,
      countryOfBirthOptions,
      genderOptions,
      nationalityOptions,
      secondNationalityOptions,
      sectionOptions,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "@/styles/form-styles.scss";
</style>
