<template>
    <div>
  <input
    type="text"
    :id="id"
    :placeholder="placeholder"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
  </div>
</template>

<script setup>
const props = defineProps({
  modelValue: String,
  label: { type: String, default: 'Text Field' },
  id: { type: String, default: 'text-field' },
  placeholder: { type: String, default: 'Enter text here...' }
});
</script>

<style scoped>
label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: bold;
  text-align: center;
}
input {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  border-radius: 8px;
  border: 1px solid #ccc;
  width: 100%;
  background: #fff;
}       

</style>