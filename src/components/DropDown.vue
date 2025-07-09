<!-- components/BaseSelect.vue -->
<script setup>
const props = defineProps({
  modelValue: [String, Number],
  options: {
    type: Array,
    required: true,
  },
  placeholder: {
    type: String,
    default: 'בחר מהרשימה',
  },
});
const emit = defineEmits(['update:modelValue']);

function handleChange(event) {
  emit('update:modelValue', event.target.value);
}
</script>

<template>
  <select :value="modelValue" @change="handleChange">
    <option disabled value="">{{ placeholder }}</option>
    <option
      v-for="option in options"
      :key="option"
      :value="option"
    >
      {{ option }}
    </option>
  </select>
</template>

<style scoped>
select {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  border-radius: 8px;
  border: 1px solid #ccc;
  width: 30%;
  background: #fff;
}
</style>
