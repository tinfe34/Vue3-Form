<template>
  <div class="form-group px-5">
    <label :for="name" class="form-label">{{ label }}</label>
    <select
      v-model="value"
      :name="name"
      :id="name"
      :class="['form-select', errorMessage ? 'is-invalid' : '']"
    >
      <option value="" disabled selected></option>
      <option value="male">Male</option>
      <option value="female">Female</option>
    </select>
    <div class="invalid-feedback">{{ errorMessage }}</div>
  </div>
</template>

<script setup>
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
