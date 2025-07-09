<template>
  <h1>{{ title }}</h1>
</template>

<script setup>

defineProps({
  title: {
    type: String,
    default:"Page Title",
  },
});
</script>

<style scoped>
h1 { 
  color: #42b983;
  font-size: 2em;
  margin-bottom: 20px;
  text-align: center;
}   
</style>