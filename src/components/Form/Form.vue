<template>
  <div class="form-donate">
    <div class="container my-lg-5">
      <div class="row g-0">
        <div class="col-12 col-lg-3">
          <BackgroundForm />
        </div>
        <div class="col-12 col-lg-9">
          <form class="form-donate__form my-5" @submit="onSubmit">
            <div class="row gx-0">
              <div class="col-12 col-lg-6">
                <InputText name="first_name" label="First Name" />
              </div>
              <div class="col-12 col-lg-6">
                <SelectOption name="gender" label="Gender" />
              </div>
              <div class="col-12 col-lg-6">
                <InputText name="last_name" label="Last Name" />
              </div>
              <div class="col-12 col-lg-6">
                <div class="form-group px-5">
                  <label class="form-label">Payment Mode</label>
                  <div class="form-checks">
                    <InputRadio
                      type="radio"
                      inputVal="visa"
                      name="payment_mode"
                      label="Visa"
                    />
                    <InputRadio
                      type="radio"
                      inputVal="mastercard"
                      name="payment_mode"
                      label="Mastercard"
                    />
                    <InputRadio
                      type="radio"
                      inputVal="amex"
                      name="payment_mode"
                      label="Amex"
                    />
                    <div class="invalid-feedback">{{ errorMessage }}</div>
                  </div>
                </div>
              </div>

              <div class="col-12 col-lg-6">
                <InputText name="company" label="Company" />
              </div>
              <div class="col-12 col-lg-6">
                <InputText
                  name="card_number"
                  label="Card Number"
                  type="number"
                />
              </div>
              <div class="col-12 col-lg-6">
                <InputText name="email" label="Email" type="email" />
              </div>
              <div class="col-12 col-lg-6">
                <InputText name="expiration" label="Expiration" />
              </div>
              <div class="col-12 col-lg-6">
                <InputText
                  name="phone_number"
                  label="Phone Number"
                  type="number"
                />
              </div>
              <div class="col-12 col-lg-6">
                <InputText name="cnv" label="Cnv" />
              </div>
              <div class="col-12">
                <RangeSlider name="donate_us" label="Donate Us" />
              </div>
              <div class="col-12">
                <div
                  class="d-grid gap-2 d-md-flex justify-content-md-end px-5 mb-4"
                >
                  <BaseButton class="btn-primary" type="submit"
                    >SUBMIT</BaseButton
                  >
                  <BaseButton
                    class="btn-outline-secondary"
                    type="button"
                    @click="handleReset"
                    >Reset</BaseButton
                  >
                </div>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import { computed } from "vue";
import { useForm } from "vee-validate";
import * as yup from "yup";

//components
import InputText from "../InputText/InputText.vue";
import SelectOption from "../SelectOption/SelectOption.vue";
import RangeSlider from "../RangeSlider/RangeSlider.vue";
import BackgroundForm from "../BackgroundForm/BackgroundForm.vue";
import InputRadio from "../InputRadio/InputRadio.vue";
import BaseButton from "../Button/BaseButton.vue";

export default {
  setup() {
    const formValues = {
      donate_us: "500",
      payment_mode: "visa",
    };

    const schema = computed(() => {
      return yup.object().shape({
        first_name: yup.string().required().label("First Name"),
        last_name: yup.string().required().label("Last Name"),
        company: yup.string().required().label("Company"),
        email: yup.string().required().email().label("Email"),
        phone_number: yup.string().required().label("Phone Number"),
        card_number: yup.string().required().label("Card Number"),
        expiration: yup.string().required().label("Expiration"),
        cnv: yup.string().required().label("Cnv"),
        payment_mode: yup.string().required("A radio option is required"),
        gender: yup.string().required().label("Gender"),
      });
    });

    const { handleSubmit, values, resetForm, handleReset } = useForm({
      validationSchema: schema,
      initialValues: formValues,
    });

    const onSubmit = handleSubmit((values) => {
      window.localStorage.setItem("form_donate", JSON.stringify(values));
      resetForm();
    });

    return { onSubmit, handleReset, values };
  },

  components: {
    Form,
    Field,
    ErrorMessage,
    RangeSlider,
    InputText,
    SelectOption,
    BackgroundForm,
    InputRadio,
    BaseButton,
  },
  computed: {},
  methods: {},
};
</script>

<style lang="scss">
@import "./Form.scss";
</style>
