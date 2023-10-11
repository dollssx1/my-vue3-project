<script setup>
import { computed } from 'vue'

const props = defineProps({
  modelValue: { required: true, type: String },
  modelModifiers: { default: () => ({}) }
})

const emit = defineEmits(['update:modelValue'])

const value = computed({
  get() {
    return props.modelValue
  },
  set(value) {
    if (value) {
      emit('update:modelValue', value)
    }
  }
})

function emitValue(e) {
  let value = e.target.value
  if (props.modelModifiers.capitalize) {
    value = value.charAt(0).toUpperCase() + value.slice(1)
  }
  emit('update:modelValue', value)
}
</script>

<template>
  <input v-model="value" @input="emitValue" />
</template>
