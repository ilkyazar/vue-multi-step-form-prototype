<template>
  <h2 class="form-header">Contact Info</h2>
  <div class="form-body">
    <Form :validation-schema="schema" v-slot="{ errors }">
      <h3 class="form-header">Registration address</h3>
      <InputFormField
        labelName="Street"
        fieldName="street"
        :error="errors.street"
        @input="$emit('update:street', $event.target.value)"
        :inputValue="street"
      />
      <InputFormField
        labelName="House Number"
        fieldName="houseNumber"
        :error="errors.houseNumber"
        @input="$emit('update:houseNumber', $event.target.value)"
        :inputValue="houseNumber"
      />
      <InputFormField
        labelName="Postal Code"
        fieldName="postalCode"
        :error="errors.postalCode"
        @input="$emit('update:postalCode', $event.target.value)"
        :inputValue="postalCode"
      />
      <InputFormField
        labelName="Location"
        fieldName="location"
        :error="errors.location"
        @input="$emit('update:location', $event.target.value)"
        :inputValue="location"
      />
      <DropdownFormField
        :options="countryOptions"
        labelName="Country"
        fieldName="country"
        :error="errors.country"
        @input="$emit('update:country', $event.target.value)"
        :inputValue="country"
      />
      <div class="form-field">
        <label
          ><input type="checkbox" v-model="secondAddressChecked" />Delivery
          Address</label
        >
      </div>
      <div class="optional-contact-address" v-if="secondAddressChecked">
        <h3 class="form-header">Delivery Address</h3>
        <InputFormField
          labelName="Street"
          fieldName="secondAddressStreet"
          :error="errors.secondAddressStreet"
          @input="$emit('update:secondAddressStreet', $event.target.value)"
          :inputValue="secondAddressStreet"
        />
        <InputFormField
          labelName="House Number"
          fieldName="secondAddressHouseNumber"
          :error="errors.secondAddressHouseNumber"
          @input="$emit('update:secondAddressHouseNumber', $event.target.value)"
          :inputValue="secondAddressHouseNumber"
        />
        <InputFormField
          labelName="Postal Code"
          fieldName="secondAddressPostalCode"
          :error="errors.secondAddressPostalCode"
          @input="$emit('update:secondAddressPostalCode', $event.target.value)"
          :inputValue="secondAddressPostalCode"
        />
        <InputFormField
          labelName="Location"
          fieldName="secondAddressLocation"
          :error="errors.secondAddressLocation"
          @input="$emit('update:secondAddressLocation', $event.target.value)"
          :inputValue="secondAddressLocation"
        />
        <DropdownFormField
          :options="countryOptions"
          labelName="Country"
          fieldName="secondAddressCountry"
          :error="errors.secondAddressCountry"
          @input="$emit('update:secondAddressCountry', $event.target.value)"
          :inputValue="secondAddressCountry"
        />
      </div>
      <InputFormField
        labelName="Phone Number"
        fieldName="phoneNumber"
        :error="errors.phoneNumber"
        @input="$emit('update:phoneNumber', $event.target.value)"
        :inputValue="phoneNumber"
      />
      <div class="form-field">
        <label
          ><input type="checkbox" v-model="landlineNumberChecked" />Landline
          Number (optional)</label
        >
      </div>
      <div class="optional-phone-number" v-if="landlineNumberChecked">
        <InputFormField
          labelName="Landline Number"
          fieldName="landlineNumber"
          :error="errors.landlineNumber"
          @input="$emit('update:landlineNumber', $event.target.value)"
          :inputValue="landlineNumber"
        />
      </div>
      <InputFormField
        labelName="E-Mail Address"
        fieldName="email"
        :error="errors.email"
        @input="$emit('update:email', $event.target.value)"
        :inputValue="email"
      />
    </Form>
  </div>
</template>

<script>
import { Form } from "vee-validate";
import InputFormField from "@/components/form-fields/InputFormField.vue";
import DropdownFormField from "@/components/form-fields/DropdownFormField.vue";
import * as Yup from "yup";
import { markRaw } from "vue";
import { ref } from "vue";

export default {
  name: "AddressForm",
  components: {
    Form,
    InputFormField,
    DropdownFormField,
  },
  props: {
    street: {
      type: String,
    },
    houseNumber: {
      type: String,
    },
    postalCode: {
      type: String,
    },
    location: {
      type: String,
    },
    country: {
      type: String,
    },
    secondAddressStreet: {
      type: String,
    },
    secondAddressHouseNumber: {
      type: String,
    },
    secondAddressPostalCode: {
      type: String,
    },
    secondAddressLocation: {
      type: String,
    },
    secondAddressCountry: {
      type: String,
    },
    phoneNumber: {
      type: String,
    },
    landlineNumber: {
      type: String,
    },
    email: {
      type: String,
    },
  },
  setup() {
    const schema = markRaw(
      Yup.object().shape({
        street: Yup.string().required("Street is required"),
        houseNumber: Yup.string().required("House Number is required"),
        postalCode: Yup.string().required("Postal Code is required"),
        location: Yup.string().required("Location is required"),
        country: Yup.string().required("Land is required"),
        phoneNumber: Yup.string().required("Phone Number is required"),
        landlineNumber: Yup.string(),
        email: Yup.string()
          .email("Must be a valid E-Mail Address")
          .max(255)
          .required("E-Mail Address is required"),
      })
    );
    const countryOptions = ref(["Germany", "Belgium", "Netherlands"]);
    const secondAddressChecked = ref(false);
    const landlineNumberChecked = ref(false);
    return {
      schema,
      countryOptions,
      secondAddressChecked,
      landlineNumberChecked,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "@/styles/form-styles.scss";
</style>
