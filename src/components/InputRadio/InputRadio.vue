<template>
  <div class="form-check form-check-inline">
    <input
      type="radio"
      v-model="value"
      :value="inputVal"
      :id="inputVal"
      :name="name"
      class="form-check-input"
      :checked="value === inputVal"
    />
    <label class="form-check-label" :for="inputVal">{{ label }}</label>
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
    default: "radio",
  },
  isChecked: {
    type: Boolean,
    default: false,
  },
  inputVal: {
    type: String,
  },
});

const nameRef = toRef(props, "name");
const { errorMessage, value } = useField(nameRef);
</script>
