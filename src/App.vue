<script setup>
  import InputTag from './components/InputTag.vue'
  function handleOntagsChange(tags) {
    console.log(tags)

  }
</script>

<template>
  <InputTag @onTagsChange="handleOntagsChange" />
</template>

<style scoped></style>
