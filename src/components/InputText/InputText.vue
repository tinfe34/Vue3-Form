<template>
  <div class="form-group px-5">
    <label :for="name" class="form-label">{{ label }}</label>
    <input
      v-model="value"
      :type="type"
      :id="name"
      :class="['form-control', errorMessage ? 'is-invalid' : '']"
    />
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
