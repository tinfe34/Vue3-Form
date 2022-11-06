<template>
  <div class="form-group px-5">
    <label for="donate_us" class="form-label">{{label}}</label>
    <VueSlider
      v-model="value"
      min="0"
      max="1000"
      :interval="10"
      :tooltip="'none'"
      :process-style="{ backgroundColor: '#319e5e' }"
      :dotSize="[90, 30]"
    >
      <template v-slot:dot="{ value, focus }">
        <div :class="['custom-dot', { focus }]">
          <i class="bi bi-chevron-left"></i>
          {{ `$ ${value}` }}
          <i class="bi bi-chevron-right"></i>
        </div>
      </template>
    </VueSlider>
    <div class="invalid-feedback">{{ errorMessage }}</div>
  </div>
</template>

<script setup>
import VueSlider from "vue-slider-component";
import { defineProps, toRef } from "vue";
import { useField } from "vee-validate";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  label: {
    type: String,
  },
  type: {
    type: String,
    default: "text",
  },
});

const nameRef = toRef(props, "name");
const { errorMessage, value } = useField(nameRef);
</script>
