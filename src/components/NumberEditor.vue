<script setup lang="ts">
import { computed } from 'vue'
import type { JSONSchema7 } from 'json-schema'

const model = defineModel()

const props = defineProps<{
  disabled?: boolean
  schema?: JSONSchema7
}>()

const schema = computed(() => {
  return props.schema ?? {}
})
</script>

<template>
  <span class="number-editor">
    <input
      type="number"
      v-model.lazy="model"
      :disabled="disabled"
      :min="schema.minimum"
      :max="schema.maximum"
      :placeholder="schema.title"
      :step="schema.multipleOf"
    />
    <input
      type="range"
      v-if="schema.minimum != null && schema.maximum != null"
      v-model.lazy="model"
      :disabled="disabled"
      :min="schema.minimum"
      :max="schema.maximum"
      :step="schema.multipleOf"
    />
  </span>
</template>
