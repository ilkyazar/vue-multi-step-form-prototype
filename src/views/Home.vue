<template>
  <Wizard :formData="formData" @submit="handleSubmit">
    <Step stepTitle="Step 1" stepKey="PersonalInfoForm">
      <PersonalInfoForm
        v-model:formData="formData"
        v-model:firstName="formData.firstName"
        v-model:lastName="formData.lastName"
        v-model:birthday="formData.birthday"
        v-model:birthPlace="formData.birthPlace"
        v-model:countryOfBirth="formData.countryOfBirth"
        v-model:gender="formData.gender"
        v-model:nationality="formData.nationality"
        v-model:secondNationality="formData.secondNationality"
      />
    </Step>
    <Step stepTitle="Step 2" stepKey="ContactInfoForm">
      <ContactInfoForm
        v-model:street="formData.street"
        v-model:houseNumber="formData.houseNumber"
        v-model:postalCode="formData.postalCode"
        v-model:location="formData.location"
        v-model:country="formData.country"
        v-model:secondAddressStreet="formData.secondAddressStreet"
        v-model:secondAddressHouseNumber="formData.secondAddressHouseNumber"
        v-model:secondAddressPostalCode="formData.secondAddressPostalCode"
        v-model:secondAddressLocation="formData.secondAddressLocation"
        v-model:secondAddressCountry="formData.secondAddressCountry"
        v-model:phoneNumber="formData.phoneNumber"
        v-model:landlineNumber="formData.landlineNumber"
        v-model:email="formData.email"
      />
    </Step>
    <Step stepTitle="Step 3" stepKey="ProductInfoForm">
      <ProductOverviewForm
        v-model:conditions="formData.conditions"
        v-model:productFeatures="formData.productFeatures"
      />
    </Step>
    <Step stepTitle="Step 4" stepKey="TaxInformationForm">
      <TaxInformationForm
        v-model:taxId="formData.taxId"
        v-model:taxResidency="formData.taxResidency"
      />
    </Step>
  </Wizard>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Wizard from "@/components/Wizard.vue";
import Step from "@/components/Step.vue";
import PersonalInfoForm from "@/views/forms/PersonalInfoForm.vue";
import ContactInfoForm from "@/views/forms/ContactInfoForm.vue";
import ProductOverviewForm from "@/views/forms/ProductOverviewForm.vue";
import TaxInformationForm from "@/views/forms/TaxInformationForm.vue";
import { ref } from "vue";

export default defineComponent({
  name: "Home",
  components: {
    Wizard,
    Step,
    PersonalInfoForm,
    ContactInfoForm,
    ProductOverviewForm,
    TaxInformationForm,
  },
  setup() {
    const formData = ref({
      firstName: "",
      lastName: "",
      birthday: null,
      birthPlace: "",
      countryOfBirth: "",
      gender: "",
      nationality: "",
      secondNationality: "",
      maritalStatus: "",
      employmentStatus: "",
      occupationalGroup: "",
      section: "",
      street: "",
      houseNumber: "",
      postalCode: "",
      location: "",
      country: "",
      secondAddressStreet: "",
      secondAddressHouseNumber: "",
      secondAddressPostalCode: "",
      secondAddressLocation: "",
      secondAddressCountry: "",
      phoneNumber: "",
      landlineNumber: "",
      email: "",
      conditions: "",
      productFeatures: "",
      taxId: "",
      taxResidency: "",
    });

    function handleSubmit(e: any) {
      console.log("submit:", e);
    }

    return {
      formData,
      handleSubmit,
    };
  },
});
</script>
