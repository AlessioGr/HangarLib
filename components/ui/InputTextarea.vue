<script lang="ts" setup>
import { computed } from "vue";
import { useValidation } from "~/lib/composables/useValidationHelpers";
import { ValidationRule } from "@vuelidate/core";
import InputWrapper from "~/lib/components/ui/InputWrapper.vue";

const emit = defineEmits<{
  (e: "update:modelValue", value: string): void;
}>();
const value = computed({
  get: () => props.modelValue,
  set: (val) => emit("update:modelValue", val),
});
const props = defineProps<{
  modelValue: string;
  label?: string;
  counter?: boolean;
  maxlength?: number;
  loading?: boolean;
  messages?: string[];
  errorMessages?: string[];
  disabled?: boolean;
  rules?: ValidationRule<string | undefined>[];
}>();

const errorMessages = computed(() => props.errorMessages);
const { v, errors, hasError } = useValidation(props.label, props.rules, value, errorMessages);
</script>

<template>
  <InputWrapper
    v-slot="slotProps"
    :errors="errors"
    :messages="messages"
    :has-error="hasError"
    :counter="counter"
    :maxlength="maxlength"
    :loading="loading || v.$pending"
    :label="label"
    :value="value"
    :disabled="disabled"
  >
    <textarea v-model="value" v-bind="$attrs" :maxlength="maxlength" :class="slotProps.class" :disabled="disabled" @blur="v.$touch()" />
  </InputWrapper>
</template>

<style>
textarea {
  resize: none;
}
</style>
